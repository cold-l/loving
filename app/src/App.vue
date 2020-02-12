<template>
    <div id="app">
        <StyleEditor ref="styleEditor" :code="currentStyle"></StyleEditor>
        <ResumeEditor ref="resumeEditor" :markdown="currentMarkdown" :enableHtml="enableHtml"></ResumeEditor>
    </div>
</template>
<script>
import StyleEditor from './components/StyleEditor'
import ResumeEditor from './components/ResumeEditor'
import './assets/reset.css'
let isPc = (function() {
    var userAgentInfo = navigator.userAgent;
    var Agents = ["Android", "iPhone",
        "SymbianOS", "Windows Phone",
        "iPad", "iPod"
    ];
    var flag = true;
    for (var v = 0; v < Agents.length; v++) {
        if (userAgentInfo.indexOf(Agents[v]) > 0) {
            flag = false;
            break;
        }
    }
    return flag;
}());
let getDateDiff = function(startDate, endDate) {
    var startTime = new Date(Date.parse(startDate.replace(/-/g, "/"))).getTime();
    var endTime = new Date(Date.parse(endDate.replace(/-/g, "/"))).getTime();
    var dates = Math.abs((startTime - endTime)) / (1000 * 60 * 60 * 24);
    return dates;
}
document.title += getDateDiff((new Date()).getFullYear() + '-' + ((new Date()).getMonth() + 1) + '-' + (new Date()).getDate(), '2016-09-16') + 1 + '天';
export default {
    name: 'app',
    components: {
        StyleEditor,
        ResumeEditor
    },
    data() {
        return {
            interval: 27,
            currentStyle: '',
            enableHtml: false,
            fullStyle: [
                `/*
* Hi！
* 今天我就要来秀一波操作
* 我是个后端工程师。俗称程序员。
* 如这个页面。就是个什么也没有的网页。
* 我的工作就是给这种空白的页面加点儿东西。
* 嗯。说起来手机和电脑还得区分一下。
* 你现在用的是......[[[[检测一下]]]]......${isPc ? '电脑' : '手机'}
*/

/* 首先给所有元素加上过渡效果 */
* {
  -webkit-transition: all .3s;
  transition: all .3s;
}
/* 白色背景太单调了。来点背景 */
html {
  color: rgb(222,222,222);
  background: rgb(0,43,54); 
}
/* 文字太近了 */
.styleEditor {
  padding: .5em;
  border: 1px solid;
  margin: .5em;
  overflow: auto;
  ${ isPc ? 'width: 48%;height: 96%;' : 'width: 96%;height: 50%;' }
  font-size: 14px;
  line-height:1.5;
}
/* 这些代码颜色都一样。加点儿高亮区别来 */
.token.selector{ color: rgb(133,153,0) }
.token.property{ color: rgb(187,137,0) }
.token.punctuation{ color: yellow }
.token.function{ color: rgb(42,161,152) }
.token.comment{ color: rgb(177,177,177) }
/* 加个 3D 效果 */
html{
  -webkit-perspective: 1000px;
          perspective: 1000px;
}
.styleEditor {
  position: fixed; 
  ${ isPc ? 'left: 0;' : 'left:0;right:0;margin:auto;'}
  top: 0; 
  -webkit-transition: none; 
  transition: none;   
  ${ isPc ? '-webkit-transform: rotateY(10deg) translateZ(-100px) ;transform: rotateY(10deg) translateZ(-100px) ;' : '-webkit-transform: rotateX(-10deg) translateZ(-100px) ;transform: rotateX(-10deg) translateZ(-100px) ;' }
  ${ isPc ? '' : '-webkit-transform-origin: 50% 0% 0;transform-origin: 50% 0% 0;' }
}

/* 再来一张信纸 */
.resumeEditor{
  position: fixed; 
  ${ isPc ? 'right: 0;' : 'left:0;right:0;margin:auto;'}
  ${ isPc ? 'top: 0;' : 'bottom:2%;'}
  padding: .5em;  
  ${ isPc ? 'margin: .5em;' : ''}
  ${ isPc ? 'width: 48%;height: 96%;' : 'width: 96%;height: 50%;' }
  border: 1px solid;
  color: #222;
  overflow: auto;
  font-size: 14px;
  line-height:1.5;
  ${ isPc ? '-webkit-transform: rotateY(-10deg) translateZ(-100px) ;transform: rotateY(-10deg) translateZ(-100px) ;' : '-webkit-transform: rotateX(10deg) translateZ(-100px) ;transform: rotateX(10deg) translateZ(-100px) ;' }
    ${ isPc ? '' : '-webkit-transform-origin: 50% 0% 0;transform-origin: 50% 0% 0;' }
  }
/* 我开始写了 */


`,
                `
/* 是不是看着很简陋粗糙？
 * 因为这是 Markdown 格式的
 * 一种程序员用来写文档日志的简易语言
 * 翻译成 网页 就行了
 */
`,
                `
/* 再加点样式 */
.resumeEditor{
  padding: 2em;
  line-height:1.8;
}
.resumeEditor h2{
  display: inline-block;
  border-bottom: 1px solid;
  margin: 1em 0 .5em;
  font-size:18px;
}
.resumeEditor ul,.resumeEditor ol{
  list-style: none;
}
.resumeEditor ul> li::before{
  content: '•';
  margin-right: .5em;
}
.resumeEditor ol {
  counter-reset: section;
}
.resumeEditor ol li::before {
  counter-increment: section;            
  content: counters(section, ".") " ";  
  margin-right: .5em;
}
.resumeEditor blockquote {
  margin: 1em;
  padding: .5em;
  background: rgba(221,221,221,.5);
}

/* OK。完成！ */

`
            ],
            currentMarkdown: '',
            fullMarkdown: `全自动启动------------
----

2016年08月16日。这么多年,群主甚是感动。

已有 \`${getDateDiff((new Date()).getFullYear()+'-'+((new Date()).getMonth()+1)+'-'+(new Date()).getDate(),'2016-08-16') + 1}\` 天


------------------------------------------------------------------------------------------------------------
     有一种称呼叫“兄弟”，有一种关系叫“手足”，有一种说法叫“兄弟如手足”
     。作为八零后的我有幸体会这种关系，年龄较长的哥哥为七零后，和我有着六岁
     的年龄差距。

　　 回想小时候，生活在八、九十年代的我们与同处于同一时期的大多数家庭一样较
为清贫，我的多数衣服、鞋子都是哥哥穿剩下的。这样的环境哪像现在的小孩有着丰富
的课余生活，兄弟俩同在一个屋檐下成长，哥哥既是玩伴，又是老师，教会我许多东西
，可说是我童年、少年时期崇拜的偶像——哥哥怎么懂得这么多？作业不会做，就按惯
例请教哥哥以求解决；书本外的知识也从他那里得知不少，譬如曹植的《七步诗》我是
从哥哥那里学到的，虽说不能领悟其中的含义，但是知道了有这么一首诗；足球是哥哥
培养我养成的一大业余爱好——踢球是他教我学会踢的，看球是他引导我观看的，为此
哥俩不少被父母责骂，骂我们不务正业——那时候读书学习才是硬道理；偷摘邻居家树
上成熟的李子而被邻居责备也是受哥哥的怂恿而犯下的过错；就连懵懂的少男少女关系
也是稀里糊涂地听他饶有兴致地介绍，在我年幼的心目中播下了青春的种子……

　　 如今，我们兄弟俩都已成家立业，生活环境比小时候好了许多，相互间的话语却少
了许多，不知道是不是没有共同话题的缘故。互通电话也是以“有事吗”为开场白，并
且通话时间不会超过三分钟，准确的说大多数在一分钟之内就结束。当然了事态不可能
发展成为《七步诗》里描述的“本是同根生，相煎何太急”那样恶劣，因为我们没有发
生过所谓的不可调和的利益冲突，再则从小就被身为教师的父亲谆谆教导“兄弟同心，
其利断金”，所以不会做出出格之事，只是给人感觉是淡了些。对此，父亲分析很透彻
：“你们兄弟俩都已经成家，身后是自己的家庭，万事都会以各自家庭为出发点。”是
啊，由原来单纯的兄弟关系，加上了妯娌关系，还有家庭关系，确实复杂了许多，就连
法律也将此种关系区别于“直系血亲”而定性为“旁系血亲”。

　　 这种关系一直延续着，我们都习以为常，不想改变，也无从改变，大家的境界都提
升很高——成为了“世外高人”。日子就这样日复一日、年复一年的消逝。然而“天有不
测风云，人有旦夕祸福”，一帆风顺的哥哥由于理想高于现实，独自郁闷，继而暴饮暴食
，其结果是患上糖料病，雪上加霜的是对突如其来的疾病毫无思想准备，工作上不得志加
上身体上的疾病，使得哥哥长期睡不着觉，恶性发展成为精神分裂症。由于我们居住的小
县城医疗条件有限，就把哥哥转院到省城专业的精神病医院治疗。这突如其来的变故打破
了整个家庭的平静，所有的家人都为哥哥担心，自然我也不例外。我记得某个周末，我从
居住的县城专程赶到哥哥住院治疗的省城医院探望哥哥，临别之际说了不少安慰之言，可
是刚一转身就发觉自己眼眶湿润。不能在此流泪，于是我强忍着眼泪，头也不回地大步迈
出医院。好不容易上了前往回城车站的公交车，我那早已酝酿的泪水顿时夺框而出，犹如
绵绵细雨，难以抑制，只是身为七尺男儿的我不会痛哭出声，唯有无声的哭泣。根本不在
意旁人的表情，在这陌生的城市，身为陌生人的我只想回归自然——做一个有血有肉、有
情有义的人！在从省城乘客车回县城的路途中，我思绪万千：一方面为哥哥祈祷，祝福他
早日康复；另一方面又为他的病情担心，万一病情加重，该怎么办？年幼的侄女又怎么办
？对，作为兄弟，我理应照顾哥哥，不能让老迈的父母再分心来照顾他；作为叔叔，我理
当抚养侄女长大成人、供养她上学……

　　 谢天谢地！哥哥的病情在医生高明的医术和自身积极、有效的调养下，有了明显好转
，已经可以回单位上班。最近，由于我和爱人的工作调动，我们一家离开了一直生活的县城
，到一个邻近大一点的城市生活。我们兄弟的电话联系明显多了许多，即使大多数时候还是
像原先那样不超过三分钟——除了足球可以让我们谈论更多的时间，这足以让我们亲近很多
，很多……逢年过节，全家人团聚在一起，更是其乐融融。中国人在感情表达上是含蓄的，
尤其是中国男人不会轻易的整天在口头上“爱来爱去”，这不能说明我们中国人不重视感情
，相反在儒家“仁、义”思想的熏陶下，我们中国人更加注重自然感情的流露，我国有着几
千年历史的氏族关系就是以血缘关系为基础建立的，验证了血浓于水亘古不变的真理。对此
，我要发自内心的呐喊：“有兄弟真好！”

`
        }
    },
    created() {
        this.makeResume()
    },

    methods: {
        makeResume: async function() {
            await this.progressivelyShowStyle(0)
            await this.progressivelyShowResume()
            await this.progressivelyShowStyle(1)
            await this.showHtml()
            await this.progressivelyShowStyle(2)
        },
        showHtml: function() {
            return new Promise((resolve, reject) => {
                this.enableHtml = true
                resolve()
            })
        },
        progressivelyShowStyle(n) {
            return new Promise((resolve, reject) => {
                let interval = this.interval
                let showStyle = (async function() {
                    let style = this.fullStyle[n]
                    if (!style) {
                        return
                    }
                    // 计算前 n 个 style 的字符总数
                    let length = this.fullStyle.filter((_, index) => index <= n).map((item) => item.length).reduce((p, c) => p + c, 0)
                    let prefixLength = length - style.length
                    if (this.currentStyle.length < length) {
                        let l = this.currentStyle.length - prefixLength
                        let char = style.substring(l, l + 1) || ' '
                        this.currentStyle += char
                        if (style.substring(l - 1, l) === '\n' && this.$refs.styleEditor) {
                            this.$nextTick(() => {
                                this.$refs.styleEditor.goBottom()
                            })
                        }
                        setTimeout(showStyle, interval)
                    } else {
                        resolve()
                    }
                }).bind(this)
                showStyle()
            })
        },
        progressivelyShowResume() {
            return new Promise((resolve, reject) => {
                let length = this.fullMarkdown.length
                let interval = this.interval
                let showResume = () => {
                    if (this.currentMarkdown.length < length) {
                        this.currentMarkdown = this.fullMarkdown.substring(0, this.currentMarkdown.length + 1)
                        let lastChar = this.currentMarkdown[this.currentMarkdown.length - 1]
                        let prevChar = this.currentMarkdown[this.currentMarkdown.length - 2]
                        if (prevChar === '\n' && this.$refs.resumeEditor) {
                            this.$nextTick(() => this.$refs.resumeEditor.goBottom())
                        }
                        setTimeout(showResume, interval)
                    } else {
                        resolve()
                    }
                }
                showResume()
            })
        }
    }
}
</script>
<style scoped>
#app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
}

html {
    min-height: 100%;
}
.styleEditor {
    -webkit-backface-visibility: hidden;
}
</style>
