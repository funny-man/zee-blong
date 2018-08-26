  范例代码
    
    <!DOCTYPE html>
    <html>
      <head>
        <meta charset="utf-8">
        <title>zee</title>
        <style media="screen">
          .like-btn { font-size: 50px; }
        </style>
      </head>

      <body>
        <div class='wrapper'></div>
      </body>

      <script type="text/javascript">
        /* Component */
        // 抽象出父组件然后扩展子组件
        class Component {
          constructor (props = {}) {
            this.props = props // 参数做一些定制化需求：定制背景色 字体
          }
          setState (state) {
            const oldEl = this.el
            this.state = state
            this.el = this.renderDOM()
            if (this.onStateChange) this.onStateChange(oldEl, this.el)
          }
          renderDOM () {
            this.el = createDOMFromString(this.render())
            if (this.onClick) {
              this.el.addEventListener('click', this.onClick.bind(this), false)
            }
            return this.el
          }
        }
        const createDOMFromString = (domString) => {
          const div = document.createElement('div')
          div.innerHTML = domString
          return div
        }

        // 传入实例和容器然后执行实例操作
        const mount = (component, wrapper) => {
          wrapper.appendChild(component.renderDOM())
          component.onStateChange = (oldEl, newEl) => {
            wrapper.insertBefore(newEl, oldEl)
            wrapper.removeChild(oldEl)
          }
        }
        /* ========================================= */
        // 子组件
        class LikeButton extends Component {
          constructor (props) {
            super(props)
            this.state = { isLiked: false }
          }
          onClick () {
            this.setState({
              isLiked: !this.state.isLiked
            })
          }
          render () {
            return `
              <button class='like-btn' style="background-color: ${this.props.bgColor}">
                <span class='like-text'>
                  ${this.state.isLiked ? '取消' : '点赞'}
                </span>
                <span>👍</span>
              </button>
            `
          }
        }
        class RedBlueButton extends Component {
          constructor (props) {
            super(props)
            this.state = {
              color: 'red'
            }
          }
          onClick () {
            this.setState({
              color: 'blue'
            })
          }
          render () {
            return `
              <div style='color: ${this.state.color};'>${this.state.color}</div>
            `
          }
        }
        
        const wrapper = document.querySelector('.wrapper')
        mount(new LikeButton({ bgColor: 'red' }), wrapper)
        mount(new LikeButton(), wrapper)
        mount(new RedBlueButton(), wrapper)
      </script>
    </html>
