---
title: "How I Learned to Worry Less about Fake Images Online"
subtitle: "Research paper on detecting AI-generated images using convolutional neural networks"
category: Research
tags: [research, computer-vision, cnn, deepfakes, ai-detection]
order: 17
---

*Research paper by Marcus Tan, Lucas Sheldon, Sun Te, and Michael Lee.*

Despite their increasing sophistication, AI-generated images remain surprisingly easy to distinguish from authentic photographs — if you're a CNN, that is.

## Key Finding

All models achieved 99.7-99.9% validation accuracy on balanced datasets without significant overfitting. Even shallow models trained from scratch performed comparably to pre-trained networks. The detection task is, for now, far easier than generating convincing fakes.

## Why Detection Works

Here's the counterintuitive part: the CNNs aren't looking at what humans look at. Rather than relying on high-level semantic features (distorted hands, impossible proportions), the models exploit **low-level texture patterns** — fingerprints inherent to diffusion model outputs that are invisible to the human eye.

## Methodology

### Models Tested
- ResNet (18, 50, 101)
- MobileNetV2
- EfficientNet
- SqueezeNet

### Dataset
MS COCO (82,783 real training images) paired with COCOFake (413,915 synthetic images generated via Stable Diffusion v1.4 and v2.0).

### Interpretation Techniques
Guided Grad-CAM, Integrated Gradients, and SHAP value analysis were used to understand model decision-making. These consistently revealed that models focus on texture rather than semantic content.

## Imbalanced Dataset Results

When artificially skewing datasets to favor real images (up to 64:1 ratios), validation accuracy degraded from 99.9% to 91.0%. Still robust for practical applications, but a reminder that class balance matters even when the underlying signal is strong.

## Practical Implications

Platforms can effectively filter synthetic content before presenting images to users. The texture-based detection approach means that as long as generative models leave any statistical fingerprint in their outputs — which current diffusion models do — automated detection remains viable.

The open question is whether future generative models will learn to eliminate these texture artifacts. It's an arms race, but defenders currently have a significant advantage.
