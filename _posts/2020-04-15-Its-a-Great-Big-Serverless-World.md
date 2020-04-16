---
layout: post
title: It's a Great Big Serverless World
---
So I've been thinking about how you democratize serverless and enable hybrid cloud computing in the same fell stroke and Kubernetes/KNative came up once or twice. So work has me dealing with Lambdas, all cloud native development, but I'm just old school and I want to have more control than lambdas or some other proprietary solution will ever give me.

---

### **KUBERNETES**
![k8s](/assets/k8s_logo_200.png)  

Enter Kubernetes, which enables scaling to zero so it's got the same effective pricing model and availability as some serverless function, but you're not locked into some vendor. They've got Stateful Sets now so you can run MongoDB or Kafka on Kubernetes now too. It's become a pretty much universal container orchestration tool. `docker-compose` on steroids.

So I opened [an issue](https://github.com/serverless/serverless/issues/7582) on the serverless github though after trying to do it manually with docker push tag, making a `service.yaml` configuration file and applying it with `kubectl apply --filename service.yaml` in following the instructions for the [KNative getting started app](https://knative.dev/docs/serving/getting-started-knative-app/), I'm seeing `example.com` in the URL, which apparently means our DNS configuration is shit.

```bash
kubectl get ksvc my-service
NAME         URL                                     LATESTCREATED      LATESTREADY   READY   REASON
my-service   http://my-service.default.example.com   my-service-mm7tw                 False   RevisionMissing
```

And there isn't a whole lot of info on configuring DNS for microk8s right out of the box. Need to find a general example or twist a microkube example to fit my needs. Anyway this all started with me playing around with `serverless create --template knative-docker --path my-service` and it's been fun. I said I wanted to learn more about hybrid cloud and local serverless options dammit and **MEGA HYPER** `docker-compose` AKA Kubernetes said "_yeah that's me_."

I've got to figure out how to configure DNS, heck how to configure the whole system, since I want to get this serverless + knative + microk8s thing going. Already thinking about using MongoDB as a Binary weights server to AI models running in KNative services. I guess that's what Kubeflow is about though :thinking:.

---

### **SERVERLESS + KNATIVE**
![serverless + knative](/assets/serverless_plus_knative.png)  
No I never imagined I would give a fucking shit about Kubernetes configurations, but I've come to give a damn about Cloudformation and if I can do that I can quite easily start to care about the backbone of hybrid cloud computing AKA container orchestration on a level beyond what `docker-compose` can provide.

Whoa holy shit I sound boring. Look here's the thing though. People spend super megabucks on cloud computing when their computing resource needs aren't that flexible and their market share is pretty well and guaranteed, so they know what they need and the odds are stacked in their favor they aren't going belly up in the next few weeks.

Cloud computing is the elastic employee wet dream come to life. You don't have to invest in things beyond the next quarter. You could fire _everybody_ if you found another solution and it wouldn't dramatically impact your on-site infrastructure needs. It's the way tech prepares itself to be bought out and folded under by the widget bookies that buy up stock in companies and eviscerate their R & D departments in the interest of "_lean management_." So they pay out the fucking nose so management can always press the button and walk away, no questions asked. It's also why they love to use contract employees, but I digress.

Some of us aren't about all that, and it would be super awesome to be able to deploy a clone of our local cluster to the cloud in such a way as where one is there for the other. Cloud-level fault tolerance. Lower costs and development cycle times of local development. Well in my opinion anyway. I'm a bit of a control freak. No doubt about the lower costs and development cycles, but especially the costs. Design effectively infinitely scalable systems locally on the same machinery they run in the data centers.

That's the key though to making a profitable company in such a crowded space imo. Work on the interconnect between the local KNative + k8s and the instance running in the cloud, where serverless has spent considerable time and effort being an exhaustive collection of serverless platforms.

They've got the right idea, but I'm thinking more along the lines of `serverless create --template knative-docker --path my-service`, work on increasing out of the box interop between serverless, knative, gpu, and dns on microk8s, and then our tools comes along and configure settings to deploy a clone of your local system to one of $$N$$ different cloud providers, _**US**_ among them.

I want to bring integration of ROCm PyTorch and other DL frameworks running on AMD GPUs to the forefront of hybrid cloud development. I want to make it a new paradigm for backend computing and I want to figure out a way to break ROS2 out into a container orchestrated set of services to make them scalable from $$\infty$$ to zero.

Use the built in computing/networking capabilities of kubernetes to make a workaround to DDS middleware. Same end effect for users, but instead of being built on a single instance of an RTPS DDS implementation, topic sharing were wired into the computing framework.

This is worth making into a list:
- microk8s: this all starts with [microk8s](https://github.com/ubuntu/microk8s). deploy _anywhere_. effortless-ish. STELLAR DOCS
- serverless: we want to be like them. they are a middleware between developers and different serverless platforms
- knative: we want to be a middleware between knative developers and different cloud providers focused on hybrid cloud deployment

---

### **MICROK8S + KNATIVE + SERVERLESS**
![microk8s + knative + serverless](/assets/microk8s_knative_serverless.png)

#### `microk8s`
I want to bring people on board with Kubernetes my adopting MicroK8s as the official K8S distribution of our project. Holy fuck we've got a project here folks. I think I know what it was. I said it earlier.
>I want to figure out a way to break ROS2 out into a container orchestrated set of services to make them scalable from $$\infty$$ to zero. Use the built in computing/networking capabilities of kubernetes to make a workaround to DDS middleware. Same end effect for users, but instead of being built on a single instance of an RTPS DDS implementation, topic sharing were wired into the computing framework.  

I don't think Kubernetes is going anywhere. I think with using [GRPC](https://grpc.io) and swift/c++ code orchestrated in containers you can have nearly the same speeds as calling functions from `/usr/lib/libsomething.2.3.so` and it enables a level of scalability and interoperability that non-containerized solutions just simply lack.

K8S + HPC is a [hot topic](https://kubernetes.io/blog/2017/08/kubernetes-meets-high-performance/) with many apparently. I mean what is the cost of having libraries in containers really? Have you ever tried to build something that depended on PETSc? Containers are the way and the light. If we pay a little bit for each container image size we get _so much_ in terms of reproducibility and portability which ultimately leads to **SCALABILITY**.

Anyway I've gotten off topic there but the idea is to make developing libraries out of microservices that run on kubernetes clusters all the rage by putting in the extra effort to be sure it works _everywhere_ for **everybody** using whatever combination of hardware you could think of. Give them the best development environment possible that will emulate and transition seamlessly into a hybrid cloud deployment.

Linker? Do you mean `linkerd`? :joy: Something that makes flexible heterogenous beowulf clusters out of the devices it is running on so when you're plugged in and not developing, your device is doing some of the lifting. Take the _run everywhere_ philosophy of `microk8s` seriously and use it as a bridge between edge and cloud development.

#### `serverless`
When you configure your local development environment, we're getting it ready to deploy on the cloud, just like serverless. However, unlike serverless we're not going to focus on supporting a bunch of other companies' proprietary software chains. Nope. We're going to focus in on being like serverless, but in streamlining the creation of events for KNative and Kubeflow.

Yeah we might as well incorporate Kubeflow into our toolchain. We want to be able to use ROCm or OpenCL versions of pytorch and other automatic differentiation frameworks (`tensorflow swift`, `jax`) running on AMD for dirt cheap local supercomputing and the lowest prices on GPU training instances around once we get our cloud computing division up on its feet.  

#### `knative`

I yacked too much about microk8s I don't know what to say about knative. Um. That making KNative's configuration management and integration into the other addons of microk8s as seamless and painless as possible is pretty much our highest priority. Yeah we've got work to do with `gpu` to integrate AMD hardward using ROCm and OpenCL, but this is really about serverless + knative. microk8s is the platform.

I just do think that integrating tightly into a minimal kubernetes distro makes a hell of a lot of sense. Have microk8s + knative integration so effortless you don't even have to do it anymore it just comes enabled out of the box or with a single command. You know like `microk8s enable knative` is _supposed_ to do but didn't for me.

No KNative is _really, really, really_ important to the plan, which is basically to ship a microk8s superpackage/configuration script that enables all of the functionality of `serverless create --knative-docker` plus more than serverless does right now, fresh out of the box. Instead of focusing on templates for all the different proprietary serverless platforms, we hone in on knative and focus on:
1. We wrap ourselves up in microk8s. They're our default kubernetes install. Fully complete solution. serverless + the cluster manager shrunk down to a scalable single node. It's instant beowulf cloud time. Can you run a snap on it? Then it's connected to the microk8s cluster and running services. Not all the data will be coming in to be computed either. Now your IoT devices have access to the power of an ultra-low latency beowulf cluster. IoT + MicroK8s + HPC.
2. Hybrid deployment. So you've gotten your service working on your local cluster. How should you connect to the cloud? What are your constraints? Business purpose and function? We will focus in on deploying knative clusters on the cloud that interoperate with our local cloud instances of microk8s beowulf clusters as seamlessly as possible.
3. So we've yacked about what a good fit KNaive + MicroK8s is for extending compute to the edge and touched on the importance of hybrid cloud capabilites. But I really want to make all the neat things that KNative can do easily accessible to folks just starting out and not something locked away behind a wall of Silicon Valley obfuscation and gatekeeping.

---

### **CONCLUSION**

I'm such a techbro hypebeast it's ridiculous. I'm just learning about this technology and I'm like "There's gold in them thar hills!" This is why people fucking hate techbros. Oh well I really do believe in a `microk8s + knative + serverless` stack that's geared towards three things:
1. `microk8s` installation and configuration management tool.
2. Beowulf cluster management - So `microk8s` runs everywhere does it? Well let's recruit _everything_ into our cluster then.
3. Hybrid cloud computing - Integrate cloud computing resources across many vendors into your system like just other nodes in the distributed cluster.  
In other words I tried to run `serverless create --knative-docker --my-service` and I can't stop thinking about what it could mean if it works.

So it looks like I'm going to try to learn as much as possible about kubernetes configurations and try to come up with some sort of advanced microk8s quick start that will have you ready to `serverless deploy` in no time. What are we going to call our microk8s boot and config management tool? How about `microk8s_`?
```bash
python3 setup.py
serverless create --knative-docker --path my-service
cd my-service
npm install
serverless deploy
serverless local invoke -f hello
```

and `setup.py` will look something like this:
```python
from catchy_name.system_tools import configure_system
from catchy_name.install_tools import install_microk8s
from catchy_name.dns_tools import configure_dns
from catchy_name.knative_tools import configure_knative
from catchy_name.submariner_tools import configure_submariner
from catch_name.testing import test_local_cfg
from catchy_name.utils import parse_args, load_cfg, merge_cfg

from pprint import pprint

args = parse_args()
cfg = load_cfg()
cfg = merge_cfg(cfg, args)

def local_install(cfg):
    """
    """
    print("Configuring your system for microk8s...")
    cfg = configure_system(cfg)
    print("Installing microk8s...")
    cfg = install_microk8s(cfg)
    print("Configuring DNS...")
    cfg = configure_dns(cfg)
    print("Configuring your system for knative...")
    cfg = configure_knative(cfg)
    print("Configuring submariner...")
    cfg = configure_submariner(cfg)
    return cfg

  .
  .
  .

def main(cfg):
    """
    """
    if cfg["local_only"]:
        cfg = local_install(cfg)
        assert test_local_cfg(cfg), f"Something went wrong installing {cfg}"
    else:
          .
          .
          .
    print("microk8s has been installed and configured successfully!")
    return cfg

if __name__ == "__main__":
  cfg = main(cfg)
  pprint(cfg)
```
oh yeah you know we're going to work with `submariner`! This is a hybrid cloud project!

![submariner](/assets/logo-submariner.png)

So the idea is to first be able to setup the system for microk8s, install microk8s, configure DNS, configure and install knative, then go ahead and preemptively configure the system for connecting to submariner in the near future after the initial **RUN LOCALLY** part of the walkthrough is done and the person going through the introductory tutorial.

They don't need to know that `salt` and `submariner` are there right at there fingertips ready to duplicate what they've just done as many machines as you want it to and tune them into a wheeling dealing hybrid cloud multicluster until they've got the hello world part of their docker code up and running as knative service locally.

![salt](/assets/saltstack.jpeg)
