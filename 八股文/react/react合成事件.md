SyntheticEvent

为了跨浏览器兼容性模拟浏览器的原生事件

1.执行顺序：先冒泡到 rootElement元素上，再执行 react事件

1 .react 把 事件都绑定到 rootElement 的目的是是什么？

### 1. 提高性能

通过在根元素上使用事件委托，React 可以减少直接在 DOM 元素上绑定事件处理函数的数量。这样做减少了内存的使用，因为只需要为根元素绑定一次事件监听器，而不是为每个子元素都绑定，特别是在有大量元素需要监听事件时，这种方式能显著提高性能。

### 2. 简化事件管理

将所有事件处理函数集中管理可以简化事件的管理和清理工作。当组件卸载时，React 只需要移除根元素上的事件监听器，而不需要关心每个组件可能添加的事件监听器，这样可以避免内存泄漏的问题。

### 3. 跨浏览器兼容性

通过合成事件（SyntheticEvent）封装浏览器原生事件，React 可以提供一致的事件对象给所有事件处理函数，无论它们在哪个浏览器中运行。这样做有助于处理不同浏览器之间的事件兼容性问题，使得开发者不需要关心底层的浏览器差异。

### 4. 实现合成事件系统

事件委托是实现 React 合成事件系统的基础。通过在根元素上监听所有事件，React 可以在内部构建自己的事件处理逻辑，包括事件的封装、重用、冒泡等，这为开发者提供了更加灵活和强大的事件处理能力。

### 5. 促进组件独立性

由于事件处理函数是在根元素上统一处理的，组件不需要直接与 DOM 元素交互来绑定或触发事件，这有助于保持组件的独立性和可重用性，使得组件更容易维护和测试。

### 总结

React 把事件都绑定到根元素的做法，通过减少直接事件监听器的数量、简化事件管理、提供跨浏览器的兼容性、实现强大的合成事件系统以及促进组件独立性等方式，提高了整个框架的性能和开发效率。

2.react 合成事件和fiber的关系

React 的合成事件系统和 Fiber 架构之间存在着紧密的关系。Fiber 架构是 React 16 中引入的一种新的内部机制，旨在提高应用的性能和响应性，特别是在动画、布局和深度嵌套更新等方面。以下是合成事件系统和 Fiber 架构之间关系的几个关键点：

### 1. 事件处理和工作循环

Fiber 架构引入了一种新的工作循环，允许 React 在渲染和更新过程中更好地控制优先级。这种机制使得 React 可以在处理用户输入（如点击或键盘事件）时，暂停、中断或重新开始正在进行的工作。合成事件系统在这个架构下工作，确保事件处理函数的执行可以与 React 的渲染和更新逻辑协同工作，提高应用的响应性和性能。

### 2. 批处理更新

在合成事件处理过程中，React 会将 setState 调用批处理，以减少不必要的渲染。Fiber 架构通过引入异步渲染能力，进一步增强了这种批处理机制。这意味着在事件处理函数中触发的状态更新可以更智能地被调度和优化，从而提高应用的性能。

### 3. 事件优先级

Fiber 架构允许 React 根据任务的重要性分配不同的优先级。这种优先级机制也适用于事件处理。例如，对于用户交互产生的事件（如点击或滚动），React 可以给予更高的优先级，以确保流畅的用户体验。合成事件系统在这种架构下，能够更好地管理事件处理的优先级，确保关键的用户交互得到快速响应。

### 4. 兼容性和稳定性

Fiber 架构的设计目标之一是提高 React 应用的兼容性和稳定性。合成事件系统作为 React 应用中处理用户输入的关键部分，与 Fiber 架构紧密集成，确保即使在复杂的应用中，事件处理也能稳定可靠地工作。

### 总结

合成事件系统和 Fiber 架构之间的关系体现在对事件处理的优化、更新的批处理、事件优先级的管理以及整体应用性能的提升上。Fiber 架构为 React 应用提供了更强大的基础，使得合成事件系统能够更有效地工作，从而提升了用户交互的响应性和应用的性能。
