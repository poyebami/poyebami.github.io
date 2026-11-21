<h1>Docker vs ContainerD</h1>
Unlike Docker, Containerd's scripe is limited: it manages core container lifecycle operations such as start, stop, pause, and delete, and handles image transfer and storage. 

<h3>Docker</h3>
Docker is a comprehensive containerization platform. It covers runtime, orchestration, networking, and etc. 

<h3>ContainerD</h3>
ContainerD is a lightweight container runtime on its own separate from Docker. It uses cases is customizable container runtime for integration. 

ctr: a debugging - oriented utility included with ContainerD that is used mainly for troubleshooting. 

nerdctl: a Docker - like CLI developed for ContainerD, offereing a more comprehensive feature set for regular container operations. 

circtl: a versatile CLI tool from the Kubernetes community that works with any CRI - compatible runtime (including ContainerD and CRI-O) and is designed for debugging and inspection.


