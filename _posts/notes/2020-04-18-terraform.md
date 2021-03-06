---
layout: post
title:  ""
author: grace
categories: []
featured: false
hidden: true
---

- terraform is a configuration language across many different cloud providers
- mindshare of current state of the world?
- how to interact w/ terraform:
  - basic CLI -- look at Terraform Commands (CLI)
  - configuration files
  - also a back-end for terraform
you specify some configuraiton, create infrastructure acc. to that config, then yo ucan evolve and change that as you go
so, tf tries to figure out the state of config live right now, what you want, then tries to apply the diff
  - so, this is where back-end comes in
  - persistence for configuration
  - before: just read/write from disk and then checking that into github
    - usually includes credentials, secrets, etc.
  - after:
    - checks in a TF state file
    - a serialized format of the current state of the world
- workspaces
  - what if you want to use same config for bunch of diff envs?
    - can split it out... or, use a workspace!
    - each workspace gets its own name + TF space
    - then available as an env variable
    - terraform worksapce my  new env, then terraform apply
- vs. kubernetes? kubenetes is a coordiantion management system for docker jenkins -- still has to be configured; tf is general configuration
- tf config
  - takes directories as a primitive
  - usually have a main.tf that describes the stuff you're gonna configure (not actually required?)
  - vars.tf -- entire thing is a function; vars.tf is the arguments to the function
    - should be things you'll change on a workspace/per-env basis
- diving into main.tf
  - format: keyword, optional string, curly braces
  - inside-out from normally how you think about data and code
  - much more declarative -- this is what you expect to exist after tf has done its job
    - nothing imperative or how to do it
- tf is not forward-compatible
- most common thing interacted with is a resource
  - could be anything -- thing you want to configure or create
  - can find a billion ones for aws
    - security groups, auto balancers, ecs, ec2, s3 buckets, cloudwatch
    - resource "aws_security_group" "sg" {}
      resource [type] [var name] {}
    - aws_security_group from aws provider
    - comes separately from core terraform
    - don't use terraform less recent than 10
- can also do standard variable interpolation `${VAR_NAME}`
- a variable has to be pre-defined before used, like in the vars.tf file
- tf tries to be strongly typed -- will fail sometimes, but it's attempting!
