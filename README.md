K8s Commands
Get pods configurations
k -n name_space get pod -oyaml
To grep a word and make it bold
k -n name_space get pod -oyaml | grep -i <word> -B 20
Scheduling Priority
apiVersion: v1
kind: Pod
metadata:
  name: important
  namespace: lion
  labels:
    name: myapp
spec:
  containers:
  - name: myapp
    image: nginx:1.21.6-alpine
    resources:
      limits:
        memory: "1Gi"
        cpu: "500m"
    ports:
      - containerPort: 80
  priority: 300000000
  priorityClassName: level3

Dillinger is currently extended with the following plugins.
Instructions on how to use them in your own application are linked below.

Plugin	README
Dropbox	plugins/dropbox/README.md
GitHub	plugins/github/README.md
Google Drive	plugins/googledrive/README.md
OneDrive	plugins/onedrive/README.md
Medium	plugins/medium/README.md
Google Analytics	plugins/googleanalytics/README.md
Development
Want to contribute? Great!

Dillinger uses Gulp + Webpack for fast developing.
Make a change in your file and instantaneously see your updates!

Open your favorite Terminal and run these commands.

First Tab:

node app
Second Tab:

gulp watch
(optional) Third:

karma test
Building for source
For production release:

gulp build --prod
Generating pre-built zip archives for distribution:

gulp build dist --prod
Docker
Dillinger is very easy to install and deploy in a Docker container.

By default, the Docker will expose port 8080, so change this within the
Dockerfile if necessary. When ready, simply use the Dockerfile to
build the image.

cd dillinger
docker build -t <youruser>/dillinger:${package.json.version} .
This will create the dillinger image and pull in the necessary dependencies.
Be sure to swap out ${package.json.version} with the actual
version of Dillinger.

Once done, run the Docker image and map the port to whatever you wish on
your host. In this example, we simply map port 8000 of the host to
port 8080 of the Docker (or whatever port was exposed in the Dockerfile):

docker run -d -p 8000:8080 --restart=always --cap-add=SYS_ADMIN --name=dillinger <youruser>/dillinger:${package.json.version}
Note: --capt-add=SYS-ADMIN is required for PDF rendering.

Verify the deployment by navigating to your server address in
your preferred browser.

127.0.0.1:8000
License
MIT

Free Software, Hell Yeah!