---
layout: default
title: Evaluation Platform Reference Stack
nav_order: 70
has_children: true
---

# Evaluation Platform Reference Stack

This section describes the reference stack that can be used to run the [evaluators]({{site.baseurl}}/evaluators/evaluators) and benchmarks aggregated from them. 

It is important to note the separation between the stack that is agnostic about particular evaluations of interest, and the &ldquo;plug-in&rdquo; evaluators themselves. A set of evaluators in a given stack deployment may represent a defined benchmark for particular objectives. 

The evaluation platform is under development. It will meet the [Shared Needs for All Users]({{site.baseurl}}/user-personae/user-personae/#shared-needs-for-all-users). A theme expressed in those needs is the ability to support both running the evaluation platform for public collaborative tasks and leaderboards, as well as support private deployments for evaluating proprietary models and systems. Both offline evaluation, such as for leaderboards and research investigations, and online inference should be able to use the same stack, with appropriate scaling and hardening of the deployments, as required.

## Architecture 

Schematically, a trust and safety deployment using the reference stack with example evaluators is shown in Figure 1:

![Reference Stack schematic diagram]({{site.baseurl}}/assets/images/ref-stack.png)

**Figure 1:** Schematic architecture of a deployment.

Note that some evaluators won't use `unitxt` and some of them will not run on `lm-evaluation-harness`. This is the practical reality of the technology today. However, our hope is that the reference stack will prove so popular and so productive to use, that it will be widely adopted by teams doing evaluation R&D.

### Execution Framework

The execution framework provides mechanisms to run evaluations and benchmarks in a consistent manner, mechanisms to aggregate results, compute metrics, and report results, and logging and error recovery capabilities. 

The open-source software (OSS) components in the stack including the following projects, which have emerged as de-facto standard tools for evaluation.

* EleutherAI’s [LM Evaluation Harness](https://www.eleuther.ai/projects/large-language-model-evaluation){:target="lm-site"} (GitHub [repo](https://github.com/EleutherAI/lm-evaluation-harness){:target="lm-repo"}), a widely used, efficient evaluation platform for inference time (i.e., runtime) evaluation and for leaderboards.
* IBM’s [Unitxt](https://www.unitxt.ai){:target="unitxt"} library, the framework for individual evaluators, which has an interesting benefit that evaluators can be _declaratively_ defined and executed without the need to execute third-party, untrusted code. This supports several of the [user needs]({{site.baseurl}}/user-personae/user-personae/#shared-needs-for-all-users) involving open collaboration in a pragmatic way, without the need for running third-party evaluation code.
* Observability and metrics collection - [Arize Phoenix](https://github.com/Arize-ai/phoenix){:target="phoenix"} or other TBD toolkit. The reference stack needs to provide the desired information, but it also needs to be agnostic about the specific tools used, as different environments will have different standard tools in place already.

### Leaderboard Deployments

While supporting private, on-premise deployments for proprietary evaluation requirements, the stack will be used to implement [public leaderboards]({{site.baseurl}}/leaderboards/leaderboards/) hosted in the [AI Alliance Hugging Face Community](https://huggingface.co/aialliance){:target="hf"}.

_This is a work in progress._

## Installation for Local Experimentation

To install [LM Evaluation Harness](https://www.eleuther.ai/projects/large-language-model-evaluation){:target="lm-site"}, use the following command, from the GitHub repo [README](https://github.com/EleutherAI/lm-evaluation-harness){:target="lm-repo"}:

```shell
git clone --depth 1 https://github.com/EleutherAI/lm-evaluation-harness
cd lm-evaluation-harness
pip install -e .
```

TODO: Add a "fast" example using one or more `unitxt` evaluators.

The `lm-evaluation-harness` [README](https://github.com/EleutherAI/lm-evaluation-harness){:target="lm-repo"} have other examples and other ways to run evaluations in different deployment scenarios.
