<h1>Getting started with Docker</h1>

There are two edition of Docker. The 'enterprise' and 'community' editions. The community edition is the set of free Docker products. The enterprise edition is the certifed and supported containers platform that co mes with enterprise add-ons 
like image management, image security, universal control plane for managing and orchestrating containers runtimes. 

<h1>Setup and Install Docker</h1>
Visit docs.docker.com and select "get docker". From the left-hand menu, select your system type and follow the instructions. After installing docker, we will run a simple container to ensure everything is work.
Visit hub.docker.com. There is a list of the most populr Docker images likes Nginx, MongoDB, Alpine, Node.js, Redits, and more. For our case, we will be using a whalesay. Which is a simple application that trains a whale saying something. 
Run the command 
 ```console
 sudo docker run docker/whalesay cowsay Hello-World!
 ```
