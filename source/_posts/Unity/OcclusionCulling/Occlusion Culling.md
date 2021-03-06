# Occlusion Culling

## 介绍

* 1:[官方文档](https://connect.unity.com/doc/Manual/OcclusionCulling)
* 2:当对象被其他对象阻挡（遮挡）而不能被摄像机所看到时，遮挡剔除 (Occlusion Culling) 功能会禁用对象的渲染.这种情况不会自动发生在 3D 计算机图形中，因为在大多数时间，距离摄像机最远的对象都是先绘制的，而较近的对象则在先前对象的基础上绘制（这称为“过度绘制 (Overdraw)”）,遮挡剔除与视锥体剔除 (Frustum Culling) 不同。视锥体剔除仅禁用摄像机视野之外的对象的渲染器，而不会禁用由过度绘制隐藏起来的任何对象的渲染器。请注意，使用遮挡剔除时，仍然会受益于视锥体剔除。
* 3:工作原理:遮挡剔除过程将使用虚拟摄像机在场景中移动，进而构建潜在可见对象集的层级视图。每个摄像机在运行时都会使用此数据来识别可见和不可见的对象。凭借此信息，Unity 将确保只发送可见对象进行渲染。这样可减少绘制调用次数并提高游戏性能,遮挡剔除的数据由单元格组成。每个单元格是从整个场景包围体上细分而来。具体地来说，这些单元格形成一个二叉树。遮挡剔除使用两个树，一个用于视图单元格（静态对象），另一个用于目标单元格（移动对象）。视图单元格映射到一个定义可见静态对象的索引列表，从而为静态对象提供更准确的剔除结果。
* 4:何时应使用 Occludee Static？不会产生遮挡的完全透明或半透明对象，以及不太可能遮挡其他对象的小型对象应标记为被遮挡物 (Occludee) 而不是遮挡物 (Occluder)。这意味着，它们将被其他对象遮挡，但本身不会被视为遮挡物，这样将有助于减少计算。