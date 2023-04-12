
## commit 之前
npm run inspect (type check and lint)
npm run test:report -- -u
npm run test:report

## 命令
- lerna run test:report -- -u 更新jest测试快照

## @active/css


## react-foundation
1. update @active/css version
 npm install @active/css@latest -w @active/react-ui
## chart
AreaChart Legend
1. AreaChart => Cartesian2dChart => Chart => Legend => useLegend => SampleLegend => LegendItem => type props

## Menu
## Popper 这边拿到最外层（比如Dropdown refElement主要是去做一些元素的监听 (refElement)
1. Popper [react-popper](https://popper.js.org/docs/v2/)
2. ResizeObserver. useEffect (Popper 内部依赖问题)
  - https://blog.sethcorker.com/resize-observer-api/
  - https://codefrontend.com/resize-observer-react/
  - https://dev.to/murashow/how-to-use-resize-observer-with-react-5ff5
  - https://blog.logrocket.com/how-to-use-the-resizeobserver-api-a-tutorial-with-examples/
1. ResizeObserver
   https://developer.mozilla.org/zh-CN/docs/Web/API/ResizeObserver

### Menu
- ReactDOM.createPortal
- react.context provider

### useSelectOnlyComboBox
处理最外层的 keydown 触发的 focus blur event

comboBoxBase 
 1. ComboBox click event
 2. listBox keydown event
 3. ListBoxEscape
 4. ComponentFocus
 5. COmponentBlur(combobox & listbox)

## Popper 
1. Popper open时候组件内部会不断的render(AWF-2404)
cause root: hooks depends on 'instance'
solution: use 'selectedValue' replace 'instance' depends
scope: ColorPicker DatePicker Menu Popover Tooltip
 主要影响的是Menu  因为这个组件里面再多选时候需要动态计算Popper的元素尺寸
