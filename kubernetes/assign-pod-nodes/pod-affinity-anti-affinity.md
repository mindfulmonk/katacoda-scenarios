`NodeAffinity` allows you to schedule pods on specific nodes. But what if you want to run multiple pods on specific nodes? **`Pod affinity`** helps with that.

>**Note**: As this is a beta feature, we won't be running any of them in this exercise, however it's important to understand the basic concepts. For more information, read the Kubernetes documentation on [Affinity and Anti-Affinity](https://kubernetes.io/docs/concepts/configuration/assign-pod-node/#affinity-and-anti-affinity).

### Pod Affinity

When you look at the [Kubernetes API Reference](https://v1-10.docs.kubernetes.io/docs/reference/generated/kubernetes-api/v1.10/#podaffinity-v1-core), you'll notice that the two `specs` for Pod Affinity are:

* `spec.affinity.podAffinity.preferredDuringSchedulingIgnoredDuringExecution`is for **Soft Pod Affinity**. If the preferred option is available, the Pod will run there. If not, the Pod can still be scheduled elsewhere. 

* `spec.affinity.podAffinity.requiredDuringSchedulingIgnoredDuringExecution` is for **Hard Pod Affinity**. If the required option is not available, the Pod cannot run.

### Hard Pod Affinity

Let's inspect the `pod-hard-affinity.yaml` file:

`cat /manifests/pod-hard-affinity.yaml`{{execute}}

<p style="text-align:center;"><img src="/contino/courses/kubernetes/assign-pod-nodes/assets/pod-hard-affinity.png" alt="pod-hard-affinity"></p>


This is a `hard pod affinity`. If none of the nodes are labelled with **fruit=apple**, then the pod won't be scheduled.

The **topologyKey** is a label of a node, such as `kubernetes.io/hostname` (as seen in the picture).

### Soft Pod Affinity

Soft Pod Affinity will schedule the Pod even though is not finding a pod running with label **fruit=apple**.

### Pod Anti-Affinity

When you look at the [Kubernetes API Reference](https://v1-10.docs.kubernetes.io/docs/reference/generated/kubernetes-api/v1.10/#podantiaffinity-v1-core), you'll notice that the two `specs` for Pod Anti-Affinity are:

* `spec.affinity.podAntiAffinity.preferredDuringSchedulingIgnoredDuringExecution`is for **Soft Pod Anti-Affinity**. If the preferred option is available, the Pod will run there. If not, the Pod can still be sheduled elsewhere. 

* `spec.affinity.podAntiAffinity.requiredDuringSchedulingIgnoredDuringExecution` is for **Hard Pod Anti-Affinity**. If the required option is not available, the Pod cannot run.

`Pod anti-affinity` works the opposite way of pod affinity. If one of the nodes has a pod running with label **fruit=apple**, the pod will be scheduled on different node.

