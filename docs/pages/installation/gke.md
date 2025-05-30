---
layout: default
title: GKE
permalink: installation/kubernetes/gke
type: installation
category: kubernetes
redirect_from:
- installation/platforms/gke
display-title: "false"
language: en
list: include
image: /assets/img/platforms/gke.png
abstract: Install Meshery on Google Kubernetes Engine. Deploy Meshery in GKE in-cluster or outside of GKE out-of-cluster.
---

<h1>Quick Start with {{ page.title }} <img src="{{ page.image }}" style="width:35px;height:35px;" /></h1>

Manage your GKE clusters with Meshery. Deploy Meshery in GKE [in-cluster](#in-cluster-installation) or outside of GKE [out-of-cluster](#out-of-cluster-installation). **_Note: It is advisable to install Meshery in your GKE clusters_**

<div class="prereqs"><p><strong style="font-size: 20px;">Prerequisites</strong> </p> 
  <ol>
    <li>Install the Meshery command line client, <a href="{{ site.baseurl }}/installation/mesheryctl" class="meshery-light">mesheryctl</a>.</li>
    <li>Install <a href="https://kubernetes.io/docs/tasks/tools/">kubectl</a> on your local machine.</li>
    <li>Install <a href="https://cloud.google.com/sdk/docs/install">gCloud CLI</a>, configured for your environment.</li>
    <li>Access to an active GKE cluster in your Google Cloud project.</li>
  </ol>
</div>

Also see: [Install Meshery on Kubernetes]({{ site.baseurl }}/installation/kubernetes)

## Available Deployment Methods

- [In-cluster Installation](#in-cluster-installation)
  - [Preflight Checks](#preflight-checks)
    - [Preflight: Cluster Connectivity](#preflight-cluster-connectivity)
    - [Preflight: Plan your access to Meshery UI](#preflight-plan-your-access-to-meshery-ui)
  - [Installation: Using `mesheryctl`](#installation-using-mesheryctl)
  - [Installation: Using Helm](#installation-using-helm)
  - [Post-Installation Steps](#post-installation-steps)

# In-cluster Installation

Follow the steps below to install Meshery in your GKE cluster.

## Preflight Checks

Read through the following considerations prior to deploying Meshery on GKE.

### Preflight: Cluster Connectivity

1. Verfiy you connection to an Google Kubernetes Engine Cluster using gCloud CLI.
1. Login to GCP account using [gcloud auth login](https://cloud.google.com/sdk/gcloud/reference/auth/login).
1. After a successful login, set the Project Id:
{% capture code_content %}gcloud config set project [PROJECT_ID]
{% endcapture %}
{% include code.html code=code_content %}
1. After setting the Project Id, set the cluster context.
{% capture code_content %}gcloud container clusters get-credentials [CLUSTER_NAME] --zone [CLUSTER_ZONE] {% endcapture %}
{% include code.html code=code_content %}
1. Verify your kubeconfig's current context.
{% capture code_content %}kubectl config current-context{% endcapture %}
{% include code.html code=code_content %}

### Preflight: Plan your access to Meshery UI

1. If you are using port-forwarding, please refer to the [port-forwarding]({{ site.baseurl }}/reference/mesheryctl/system/dashboard) guide for detailed instructions.
2. If you are using a LoadBalancer, please refer to the [LoadBalancer]({{ site.baseurl }}/installation/kubernetes#exposing-meshery-serviceloadbalancer) guide for detailed instructions.
3. Customize your Meshery Provider Callback URL. Meshery Server supports customizing authentication flow callback URL, which can be configured in the following way:

{% capture code_content %}$ MESHERY_SERVER_CALLBACK_URL=https://custom-host mesheryctl system start{% endcapture %}
{% include code.html code=code_content %}

Meshery should now be running in your GKE cluster and Meshery UI should be accessible at the `EXTERNAL IP` of `meshery` service.

## Installation: Using `mesheryctl`

Use Meshery's CLI to streamline your connection to your GKE cluster. Configure Meshery to connect to your GKE cluster by executing:

{% capture code_content %}$ mesheryctl system config gke{% endcapture %}
{% include code.html code=code_content %}

Once configured, execute the following command to start Meshery.

{% capture code_content %}$ mesheryctl system start{% endcapture %}
{% include code.html code=code_content %}

If you encounter any authentication issues, you can use `mesheryctl system login`. For more information, click [here](/guides/mesheryctl/authenticate-with-meshery-via-cli) to learn more.

## Installation: Using Helm

For detailed instructions on installing Meshery using Helm V3, please refer to the [Helm Installation](/installation/kubernetes/helm) guide.

## Post-Installation Steps

Optionally, you can verify the health of your Meshery deployment, using <a href='/reference/mesheryctl/system/check'>mesheryctl system check</a>.

You're ready to use Meshery! Open your browser and navigate to the Meshery UI.

{% include_cached installation/accessing-meshery-ui.md display-title="true" %}

{% include related-discussions.html tag="meshery" %}