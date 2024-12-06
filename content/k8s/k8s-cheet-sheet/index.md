---
title: "k8s Cheet Sheet"
date: 2022-11-12T01:57:30+09:00
tags: [ k8s, Cheet sheet ]
weight: 1
description: >
  k8s用チートシート。
---

```
# すべてのPodを停止
kubectl scale --replicas=0 deployment/<your-deployment>

# Podを一つだけにする
kubectl scale --replicas=1 deployment/<your-deployment>

```
