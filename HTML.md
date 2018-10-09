#### input
- type="file" 
  - accept=".xksxm .xls" 扩展名
  - 只要是上传,就涉及到enctype
- type="button"
  - 一般用来与js结合
  - 按钮建议用<button>
- type="hidden"
  - 用于隐藏用户无需看到而又需要传递的信息.
  - 不能保存敏感数据
- type="date"
  - max="2017-09-01"
  - min="2017-09-01"
- type="datetime-local"
- type="number"
  - min max step
- type"label" 标签
  运用for属性,可用来实现联动
  或者通过嵌入label标签实现
  只要使用了checkbox或radio一定要使用label
- fieldset/legend
#### select 下拉
- option 一般第一个设为空, 不然无法选空
  - selected 设置默认选择
#### button
- 按钮上的文字不必再用value属性了,而且里面可以放图片(input的仅支持文本)
- type="button" 给js提供辅助
- type="submit"
- type="reset"
#### datalist
- 和<input list="">实现联动,带自动完成功能
  <datalist id="">
    <option>a</option>
  </datalist>  
#### form attributes
- name 用来进行前后端交互的,要事先约定好的
  以元素name的属性值为键,以元素value属性值为值,传送数据至服务器.
- placeholder 仅值为空时显示,使用提示可提高用户体验.
- disabled 不可用,提交的时候也不会将其提交到服务器中(区别于readonly,readonly的值会被提交到服务器中)
- 
