# vi: set ft=python
# docker_build('gatekeeper', '.')

repo = local_git_repo('.')
k8s_yaml(kustomize('./config/default'))

(fast_build('gatekeeper', 'Dockerfile-go', '/go/bin/manager')
  .add(repo.path('pkg/'), '/go/src/github.com/replicatedhq/gatekeeper/pkg/')
  .add(repo.path('cmd/'), '/go/src/github.com/replicatedhq/gatekeeper/cmd/')
  .add(repo.path('vendor/'), '/go/src/github.com/replicatedhq/gatekeeper/vendor/')
  .run('CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go install -a github.com/replicatedhq/gatekeeper/cmd/manager')
  .run('CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go install -a github.com/replicatedhq/gatekeeper/cmd/gatekeeper')
  .run('mv /go/bin/manager /root/manager')
  .run('mv /go/bin/gatekeeper /root/gatekeeper'))


