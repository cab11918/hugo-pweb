---
weight: 1
bookCollapsedSection: false
title: "AI文字-3D建模创作平台"
---

## AI文字-3D建模创作平台

#### 简介

这个项目的目标是利用人工智能技术支持3D建模，让整个过程更简单高效。我们致力于设计一个可靠的工具，能够比传统手工更快速地生成3D模型，从而克服了以往繁琐且耗时的问题。我们还研究了如何利用人工智能技术推动3D建模的进步，以解决相关的挑战。通过这个项目，我们希望通过AI技术显著减少人力和时间成本，提高设计师的工作效率，同时扩展设计的可能性。此外，我们计划设计一个用户友好的界面，让用户无需复杂的设计技能，只需输入文字或图片，即可轻松生成3D模型，为更多人提供创作的机会。

#### AI模型研究与选择

目前主流的几种生成方式为Point-e使用的点阵云，Shap-e使用的Nerf(Neural Radiance-field), 和谷歌的DreamFusion，还有latent-nerf... 综合生成时间，结果的质量，计算资源，还有生成风格的综合考虑，我们用谷歌云部署了DreamFusion和Shap-e，同时开发了相应的后端服务。

{{< columns >}} <!-- begin columns block -->

![Example image](/t3d1.png)

<---> <!-- magic separator, between columns -->

![Example image](/t3d2.png)

<---> <!-- magic separator, between columns -->

![Example image](/t3d3.png)

{{< /columns >}}

{{< columns >}} <!-- begin columns block -->

![Example image](/t3d4.png)

{{< /columns >}}



#### 技术选择

我们整体的服务框架是用的谷歌云。主服务后端和AI服务是分开的（主要是为了能在AI服务器不开机的情况下仍可以轻量运行其他服务）AI服务器为了方便模型的输入输出和数据处理使用了 Flask API 和 Celery 后台处理任务队列。 用户的生成结果我们保存在Firebase 然后通过Firebase Hosting部署前端代码。 最后我们链接了第三方的数据来保证用户在使用AI的同时也可以参考其他内容创作者的作品。

{{< columns >}} <!-- begin columns block -->

![Example image](/t3d5.png)

{{< /columns >}}

#### 界面

平台的主界面，以及3D模型的展示框

{{< columns >}} <!-- begin columns block -->

![Example image](/t3d6.png)

{{< /columns >}}

第三方结果和AI生成库结果的概览页面

{{< columns >}} <!-- begin columns block -->

![Example image](/t3d7.png)

{{< /columns >}}

AI生成时请求用户输入

{{< columns >}} <!-- begin columns block -->

![Example image](/t3d8.png)

{{< /columns >}}

生成结果详细信息展示

{{< columns >}} <!-- begin columns block -->

![Example image](/t3d9.png)

{{< /columns >}}





>  *（代码仓库-暂未Public）*