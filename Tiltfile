load('ext://restart_process', 'docker_build_with_restart')

docker_build_with_restart(
 'app-go',
 '.',
 dockerfile='.docker/Dockerfile',
 target='development',
 entrypoint='/app',
 only=[
  './src/',
 ],
 live_update=[
  sync('./src/web', '/web/'),
 ],
)

yaml = helm(
 './.helm',
 name='app-go',
 values=['./.helm/values-local.yaml'])

k8s_resource(
 workload='app-go-example',
 port_forwards=[
  port_forward(8000, 8000, name='api'),
 ]
)


k8s_yaml(yaml)
