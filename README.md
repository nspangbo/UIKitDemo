
# UIView

通过 `setNeedsUpdateConstraints` 告知系统需要更新约束，通常不用覆写 `updateConstraints` 方法，如果覆写，必须在最后调用 `[super updateConstraints]`。如果需要立即更新约束，也可以调用 `updateConstraintsIfNeeded`。

`scaleToFill` 通过改变宽高比，将内容填充在整个视图中，通常会发生形变，`scaleAspectFill` 在保持宽高比的情况下将内容填充在视图中，通常会有部分内容被裁减，`scaleAspectFit` 在保持宽高比的情况下，在视图中显示完整的内容，通常有部分视图区域是空白的。

`sizeThatFits` 默认实现只返回当前视图的大小，`sizeToFit` 先计算合适的视图大小，然后调整到该大小。

如果没有使用自动布局，可以通过 `setNeedsLayout` 告知系统需要布局，也可以调用 `layoutIfNeeded` 立即布局，不应该直接调用 `layoutSubviews`。如果通过代码构建 UI，并且使用自动布局技术，应该将视图的 `translatesAutoresizingMaskIntoConstraints` 属性置为 `false`。

如果使用 UIKit 或者 Core Graphics 绘制视图内容，则需要覆写 `drawRect` 方法，该方法由系统自动调用，我们应该通过 `setNeedsDisplay` 或者 `setNeedsDisplayInRect` 方法告知系统需要渲染。

当一个用户点击事件发生时，系统通过 `hitTest(_:with:)` 方法确定该事件实际发生在哪一个视图，该方法最终返回视图树种某一个分支的叶子节点视图。该方法内部通过遍历所有子视图的 `point(inside:with:)` 方法，来确认哪一个子视图应该接收事件。然后递归该过程，知道找到一个叶子节点视图。
