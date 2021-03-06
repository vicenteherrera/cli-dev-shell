# command-line-env

A cloud-native "Tardis" container image... "it's bigger in the inside".

A command line environment configured with many tools for cloud-native development and security. The container is 10+ Gb in size.

Default shell is [fish](https://fishshell.com/) with [starship](https://starship.rs/) prompt requiring a [nerd font](https://www.nerdfonts.com/) to correctly see prompt glyphs.
See `makefile` for more configuration options while building or running the image.

Aim is to include as many cloud-native tools as possible, specially if related with security. 
But the goal isn't to fill it just with plain security tools (you already have Kali Linux for that).

## Examples

After cloning this repo:

```bash
# Build using currently active user name, id and default password.
# It can take up to 30 minutes, and while installing binaries from GitHub, 
# it may return error or throttle connection. 
# Just wait and rerun picking at the last correct layer.
make build

# Run using Fish shell and sharing credential dirs (.ssh, .aws, .kube, ...), 
# and current dir as ./data
make run

# Run same but with bash shell
make run RUN_SHELL=/bin/bash
```

Without having to clone this repo:

```bash
# Run without sharing any local directory
docker run --rm -it --hostname tardis --name cli-dev-shell \
  quay.io/vicenteherrera/cli-dev-shell
```

## Software included

* [Debian 11 "Bullseye"](https://www.debian.org/News/2021/20210814)
* Containers and VM
  * [Docker](https://docs.docker.com/engine/reference/commandline/cli/) (includes 'compose' command)
  * [Podman](https://podman.io/): run container images without sudo
  * [Buildah](https://buildah.io/): build container images without sudo
  * [Skopeo](https://github.com/containers/skopeo): move container images between different types of container storages
  * [Vagrant](https://www.vagrantup.com/): virtual machines manager
  * [Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#installing-ansible-with-pip), Paramiko
  * [docker-slim](https://github.com/docker-slim/docker-slim): reduce footprint of container images
  * [docker-squash](https://github.com/goldmann/docker-squash): squash layers of a container image reducing size
  * [dive](https://github.com/wagoodman/dive): explore container image and layers
  * [act](https://github.com/nektos/act): test GitHub actions locally
  * [Docker bench](https://github.com/docker/docker-bench-security): checks for best-practices deploying Docker based on the CIS Benchmark
  * [Hadolint](https://github.com/hadolint/hadolint): dockerfile linter
* Kubernetes
  * [Kubectl](https://kubernetes.io/docs/reference/kubectl/kubectl/), [kubectl-convert](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/#install-kubectl-convert-plugin), aliases
  * [Krew](https://krew.sigs.k8s.io/)   
    * [kubectl node-shell](https://github.com/kvaps/kubectl-node-shell): start a root shell in a node    
    * [kubectl example](https://github.com/seredot/kubectl-example): resource example YAMLs
    * [kubectl neat](https://github.com/itaysk/kubectl-neat): remove clutter from manifests
    * [kubectl ktop](https://github.com/vladimirvivien/ktop): top like tool for Kubernetes
    * [kubectl nsenter](https://github.com/towolf/kubectl-nsenter): SSH onto node and spawn an nsenter shell into a pod
    * [kubectl who-can](https://github.com/aquasecurity/kubectl-who-can): shows which subjects have RBAC permissions to VERB
  * Local cluster
    * [Minikube](https://minikube.sigs.k8s.io/docs/start/): deploy a local Kubernetes cluster using different hypervisor drivers
    * [Kind](https://kind.sigs.k8s.io/): deploy a local Kubernetes cluster using Docker
    * [Minishift](https://github.com/minishift/minishift): deploy a local OpenShift cluster
  * [Kubectx, Kubens](https://github.com/ahmetb/kubectx): easely change Kubernetes config context and current namespace
  * [OpenShift 4 cli (oc)](https://docs.openshift.com/container-platform/4.7/cli_reference/openshift_cli/getting-started-cli.html)
  * [eksctl](https://eksctl.io/): create and manage EKS clusters on AWS
  * [Helm](https://helm.sh/): manage apps in Kubernetes with deploy templates packaged as charts
    * [Helm diff plugin](https://github.com/databus23/helm-diff): plugin to preview what a helm upgrade would change
  * [Helmfile](https://github.com/roboll/helmfile): deploy several Helm charts at once
  * [kops](https://kops.sigs.k8s.io/getting_started/install/): provision Kubernetes clusters on cloud providers
  * [Stern](https://github.com/wercker/stern): tail multiple pod logs on Kubernetes
  * [kubeval](https://github.com/instrumenta/kubeval): validate Kubernetes YAML using schemas generated from the Kubernetes OpenAPI specification
  * [tfk8s](https://github.com/jrhouston/tfk8s): migrate YAML manifests to the [Terraform Kubernetes Provider](https://github.com/hashicorp/terraform-provider-kubernetes)
  * [Carvel tools](https://carvel.dev/ytt/docs/v0.41.0/install/): misc tools (kapp-controller, ytt, kapp, kbld, imgpkg, vendir)
  * [kube-lineage](https://github.com/tohjustin/kube-lineage/): display all dependencies or dependents of an object in a Kubernetes cluster
  * [skaffold](https://github.com/GoogleContainerTools/skaffold): deploy source code to Kubernetes clusters building, pushing and deploying your application
  * [Artifact Hub cli (ah)](https://github.com/artifacthub/hub): lint packages for publishing them to Artifact Hub for CNCF projects
  * [Tekton cli](https://tekton.dev/docs/cli/): cli to Tekton cloud native CI/CD system
  * [Okteto cli](https://www.okteto.com/docs/cloud/okteto-cli): cli to Okteto shareable preview environments
  * [Crossplane cli](https://crossplane.io/docs/v1.9/getting-started/install-configure.html): provision, compose, and consume infrastructure using the Kubernetes API
  * [crictl](https://github.com/kubernetes-sigs/cri-tools/blob/master/docs/crictl.md): inspect and debug CRI-compatible container runtimes and applications on a Kubernetes node  
* Cloud
  * [AWS cli](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)
  * [Google Cloud cli](https://cloud.google.com/sdk/gcloud)
  * [Azure cli](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)
  * [Oracle Cloud cli](https://docs.oracle.com/en-us/iaas/Content/API/SDKDocs/cliinstall.htm)
  * [Terraform](https://github.com/hashicorp/terraform): manage cloud assest with a standard language for all providers
  * [CloudQuery](https://github.com/cloudquery/cloudquery/): query cloud resources using SQL
  * [SteamPipe](https://github.com/turbot/steampipe/): query cloud resources using SQL
  * [Cloud Custodian](https://cloudcustodian.io/docs/quickstart/index.html): query cloud assests with a standard language for all providers
* Observability
  * [promtool](https://prometheus.io/docs/prometheus/latest/configuration/unit_testing_rules/): Prometheus CLI
  * [amtool](https://github.com/prometheus/alertmanager): Alertmanager CLI
  * [pint](https://cloudflare.github.io/pint/): PromQL rule linter
  * [Robusta cli](https://docs.robusta.dev/master/installation.html): cli to Robusta Kubernetes troubleshooting and automation platform
* Cloud Native security
  * Linters
    * [kube-linter](https://github.com/stackrox/kube-linter): checks Kubernetes YAML files and Helm charts against a variety of best practices
    * [KubeAudit](https://github.com/Shopify/kubeaudit): audit Kubernetes clusters for security concerns
    * [Bad Robot](https://github.com/controlplaneio/badrobot): Kubernetes Operator static analys for high risk configurations
    * [config-lint](https://github.com/stelligent/config-lint): validate configuration files using YAML rules, including Terraform (built in), Kubernetes (using custom YAML rule files)
    * [copper](cloud66-oss/copper): validate configuration files using JS rules
    * [conftest](open-policy-agent/conftest): validate configuration files using Rego rules
  * Kubernetes general security posture analyzers
    * [Kube-hunter](https://github.com/aquasecurity/kube-hunter): hunt for security weaknesses in Kubernetes clusters
    * [Kube-score](https://github.com/zegl/kube-score): static code analysis of your Kubernetes object definitions
    * [KubeScape](https://github.com/armosec/kubescape): multi-cloud K8s risk analysis, security compliance, RBAC visualizer and image vulnerabilities scanning
    * [polaris](https://github.com/fairwindsops/polaris/): CLI to check Kubernetes pods and controllers using best practices    
    * [kubectl kubesec-scan](https://github.com/controlplaneio/kubectl-kubesec): security risk analysis
    * [kubectl score](https://github.com/zegl/kube-score): static code analysis for Kubernetes object definitions
    * [kubectl popeye](https://popeyecli.io/): scan cluster for issues
    * [kubectl doctor](https://github.com/emirozer/kubectl-doctor): scan cluster for anomalies
  * RBAC analyzers
    * [KubiScan](https://github.com/cyberark/KubiScan): Scan for risky permissions in RBAC
    * [audit2rbac](https://github.com/liggitt/audit2rbac): generate RBAC based on audit log activity
  * Supply chain
     * [cosign](https://github.com/sigstore/cosign): container signing, verification andstorage in an OCI registry
     * [in-toto](https://github.com/in-toto/in-toto): verify signed tasks in a pipeline
     * [chain-bench](https://github.com/aquasecurity/chain-bench): CIS Software Supply Chain benchmark
     * [Syft](https://github.com/anchore/syft): generate SBOM from container
     * [Vexy](https://github.com/madpah/vexy): generate VEX (Vulnerability Exploitability Exchange) in CycloneDX format
  * Container vulnerability scanners
    * [Trivy](https://github.com/aquasecurity/trivy)
    * [Grype](https://github.com/anchore/grype)
    * [Snyk](https://docs.snyk.io/snyk-cli/install-the-snyk-cli)
    * [cve-bin-tool](https://github.com/intel/cve-bin-tool)
  * Infrastructure vulnerability scanners
    * [Checkov](https://www.checkov.io/1.Welcome/Quick%20Start.html)
    * [TFScan](https://github.com/wils0ns/tfscan)
    * [Terrascan](https://github.com/tenable/terrascan#install)
  * Security platform's CLI
    * [sdc-cli](https://sysdiglabs.github.io/sysdig-platform-cli/): Sysdig CLI
    * [roxctl](https://docs.openshift.com/acs/3.66/cli/getting-started-cli.html): StackRox CLI
  * Misc
    * [detect-secrets](https://github.com/Yelp/detect-secrets): detecting secrets within a code base
    * [Illuminatio](https://github.com/inovex/illuminatio): automatically testing kubernetes network policies
    * [cmctl](https://cert-manager.io/docs/usage/cmctl/#installation): cert-manager cli
    * [Vault cli](https://www.vaultproject.io/docs/commands): secure, store and control secrets  
    * [Tetragon cli](https://github.com/cilium/tetragon): eBPF-based security observability and runtime enforcement
    * [Kubewarden cli](https://github.com/kubewarden/kwctl): policy engine for Kubernetes
* General security and networking
  * [ClamAV](http://www.clamav.net/downloads): Detect malware and virus on Windows or Linux hosts
  * [testssl.sh](https://testssl.sh): checks a server ports for TLS/SSL ciphers, protocols, recent cryptographic flaws, etc
  * [tor, torify](https://gitlab.torproject.org/tpo/team): use a different IP for requests via a p2p connection sharing network 
  * [1Password cli](https://1password.com/downloads/command-line/): cli to 1Password secret manager
  * [Yubikey manager](https://github.com/Yubico/yubikey-manager): configure Yubikey
  * [k6](https://github.com/grafana/k6): load testing tool with javascript plans
  * [apache2-utils](https://packages.debian.org/es/sid/apache2-utils): includes ab (load testing), logresolve (ip to host name), htpasswd (auth file manipulation), checkgid (test caller can configurate gid), and more.
  * [nmap](https://nmap.org/download), [ncat](https://nmap.org/ncat/), [netcat](https://sectools.org/tool/netcat/), [dig, nslookup, nsupdate](https://packages.debian.org/buster/dnsutils), [ping](https://packages.debian.org/stretch/iputils-ping)
* Programming
  * [Python](https://www.python.org/), [pip](https://pypi.org/project/pip/), [pipx](https://github.com/pypa/pipx), [PyEnv](https://github.com/pyenv/pyenv), [Poetry](https://python-poetry.org/docs/)
  * [Miniconda](https://docs.conda.io/projects/conda/en/latest/user-guide/install/linux.html): Python package manager
  * [Node](https://nodejs.org/en/), [npm](https://www.npmjs.com/), [nvm](https://github.com/nvm-sh/nvm), [npx](https://www.npmjs.com/package/npx), [yarn](https://yarnpkg.com/getting-started/)
  * [Go](https://go.dev/), [golangci-lint](https://golangci-lint.run/usage/install/#local-installation), [Ginkgo](https://github.com/onsi/ginkgo), [mockgen (Gomock)](https://github.com/golang/mock)
  * [Ruby](https://www.ruby-lang.org/en/documentation/), [Bundler](https://bundler.io/docs.html)
  * [Dot Net 6](https://docs.microsoft.com/en-us/dotnet/core/install/linux-debian)
  * Tools
    * [Jekyll](https://jekyllrb.com/): static web generator written in Ruby
    * [YAML lint](https://github.com/adrienverge/yamllint): lint YAML files
    * [Shellcheck](https://github.com/koalaman/shellcheck): lint Bash scripts
    * [mmake](https://github.com/tj/mmake): like make but prints help for targets from comments
* Shells
  * [Fish shell](https://fishshell.com/) (default)
  * Bash shell
  * zsh shell
* Command line utilities, miscelaneous
  * make, curl, wget, git, vim, nano and others...
  * [jq](https://stedolan.github.io/jq/), [yq](https://github.com/mikefarah/yq)
  * [JLess](https://github.com/PaulJuliusMartinez/jless)  
  * [GitHub cli](https://cli.github.com/)
  * [Starship prompt](https://starship.rs/): powerful shell prompt
  * [Thef*ck](https://github.com/nvbn/thefuck): correct errors in the previous console command
  * [Batcat](https://github.com/sharkdp/bat): prettier cat replacement
  * [direnv](https://direnv.net/): load and unload environment variables depending on the current directory
  * [z](https://github.com/rupa/z): smart directory changer


## Other open source Cloud Native tools for a cluster

The following Cloud Native tools should be installed in the cluster/nodes to be able to use them.

* Security
  * Runtime security
    * [Falco](https://github.com/falcosecurity/falco): runtime security based on kernel driver or eBPF
    * [Tracee](https://github.com/aquasecurity/tracee): runtime security based on eBPF
  * Security posture check
    * [KubeBench](https://github.com/aquasecurity/kube-bench): check CIS benchmarks for Kubernetes clusters
    * [Polaris](https://github.com/FairwindsOps/polaris/): admission controller to check Kubernetes pods and controllers using best practices
    * [RBAC-Police](https://github.com/PaloAltoNetworks/rbac-police): evaluate RBAC permissions of serviceAccounts, pods and nodes using Rego policies
    * [gitgat](https://github.com/scribe-public/gitgat): OPA policies that verify SCM (currently GitHub's) organization/repositories/user accounts security
  * Security Platforms (inc vulnerability assesment)
    * [ThreatMapper](https://github.com/deepfence/ThreatMapper): open source Kubernetes security platform
    * [Wazuh](https://github.com/wazuh/wazuh-kubernetes/blob/master/instructions.md): open source Kubernetes security platform
    * [SUSE Open Security Platform](https://github.com/neuvector/neuvector): formerly known as NeuVector when it wasn't open source
* Networking
  * [Calico](https://projectcalico.docs.tigera.io/about/about-calico): network security solution dataplane
  * [Istio](https://github.com/istio/istio): service mesh to integrate microservices and manage traffic flow
  * [Hubble](https://github.com/cilium/hubble): networking and security observability platform built on top of Cilium and eBPF    
* Policy / Admission Controller
  * [Gatekeeper](https://github.com/open-policy-agent/gatekeeper): admission controller OPA based
  * [Kyverno](https://github.com/kyverno/kyverno): policy engine and admission controller
  * [Kubewarden](https://github.com/kubewarden): policy engine for Kubernetes
  * [K-rail](https://github.com/cruise-automation/k-rail): workload policy enforcement to secure a multi tenant cluster
* Secrets
  * [Hashicorp Vault](https://www.vaultproject.io/)
* CI/CD / Supply chain
  * [Tekton](https://tekton.dev/docs/getting-started/#tekton-for-kubernetes-cloud-native-cicd-explained)
    * [Chains](https://github.com/tektoncd/chains): observs Tekton tasksruns completion to sign them
  * [Jenkins in Kubernetes](https://github.com/scriptcamp/kubernetes-jenkins)
  * [ArgoCD](https://github.com/argoproj/argo-cd): gitops CD platform
  * [Factory for Repeatable Secure Creation of Artifacts (FRSCA)](https://github.com/buildsec/frsca)  
  * [SPIFFE SPIRE](https://github.com/spiffe/spire): agent and server for establishing trust between software systems
  * [Notary](https://github.com/notaryproject/notary): agent and server to share signed verified content
  * [cert-manager](https://cert-manager.io/docs/usage/cmctl/#installation): certificate manager
* Observability
  * [Prometheus, Grafana, Alertmanager](https://github.com/prometheus-community/helm-charts): observability platform
  * [Robusta](https://github.com/robusta-dev/robusta): observability reporting
* Other
  * [JFrog Artifactory CE](https://jfrog.com/community/download-artifactory-oss/): binary artifact repositories
  * [GitLab CE](https://gitlab.com/gitlab-org/gitlab): software development platform with version control, issue tracking, code review, CI/CD, and more
  * [Crossplane](https://crossplane.io/docs/v1.9/getting-started/install-configure.html): provision, compose, and consume infrastructure using the Kubernetes API

## Additional tools not installed

The following tools have big requirements that would make the container image even bigger than it already is, or are meant to run graphical UI.

* [Cloud mapper](https://github.com/duo-labs/cloudmapper#installation): analyze AWS environments auditing for security issues
* [Dagda](https://github.com/eliasgranderubio/dagda): static analysis of known vulnerabilities, trojans, viruses, malware in container images and running containers on Docker.
* [Resoto](https://resoto.com/docs/getting-started/install-resoto): maps out your cloud infrastructure, generate reports, automate tasks
* [OpenSCAP base](https://www.open-scap.org/tools/openscap-base/#download): cli to parse and evaluate the SCAP standard
* [SCAP Workbench](https://www.open-scap.org/tools/scap-workbench/#download): graphical utility to perform oscap tasks
* [iamspy](https://github.com/WithSecureLabs/iamspy): load IAM policies and convert them to Z3 prover constraints and a model for querings if actions are allowed
* [GitLab cli](https://gitlab.com/gitlab-org/cli#installation)

## Other miscellaneous links:

* [Grafeas](https://grafeas.io/): metadata for software supply chain
* [Vulnerability Exploitability Exchange (VEX)](https://cyclonedx.org/capabilities/vex/): assess the exploitability of vulnerabilities in products
* [Yaradare](https://github.com/deepfence/YaRadare): YAR malware container image scanner
* [SecretScanner](https://github.com/deepfence/SecretScanner): find unprotected secrets in container images or file systems
* [PacketStreamer](https://github.com/deepfence/PacketStreamer): remote packet capture and collection tool
* [OKD](https://www.okd.io/installation/): Kubernetes distribution base for OpenShift
* [KubeAdm](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/): Kubernetes installation tool
* [k3s](k3s.io): lightweight Kubernetes installation tool
* [k0s](https://docs.k0sproject.io/v1.24.2+k0s.0/install/): lightweight Kubernetes installation tool
* [markmap](https://markmap.js.org/docs#markmap-cli): markdown mindmap generation
* [plantuml](https://plantuml.com/starting): markdown UML diagram generation
* [secwiki.cloud](https://www.secwiki.cloud/): cloud vulnerability wiki
* [cloudvulndb.org](https://www.cloudvulndb.org/): open cloud vulnerability & security issue database
* [CIRCL hashlookup](https://www.circl.lu/services/hashlookup/): free lookup hash values against known database of files (malicious/non malicious)