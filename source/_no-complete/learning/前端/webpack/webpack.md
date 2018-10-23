title: webpack打包工具
date: 2017-8-6 6:52:35
categories: js
tags: nodejs
---

<div><!--more--></div>


## webpack环境配置

npm install webpack --save-dev
npm install -g webpack

npm install vue --save
npm install vue-loader --save-dev
会自动安装vue-compiler和css-loader
npm install style-loader
npm install babel-loader --save-dev
会自动安装babel-core
npm install babel-preset-es2015 --save-dev
npm install babel-preset-stage-0 --savedev

npm install babel-plugin-transform-runtime --save-dev

如果不使用他，自己定义的函数，被多次使用，就会每次在使用这个函数的时候，就会被打包一次，使用了transform-runtime可以解决多余的代码
解决全局函数的污染，因为全局函数需要单独生成函数本省实现

缺点是：
1.无法解决实例的方法，实例的方法需要借助polyfile


使用:跟babelrc文件中使用，第二种，在packconfig.js中配置
{
	"pre
	"plugins":['transform-runtime']
}
npm install


去了解vue的运行时构建错误
alias:别名
resolve:{
	alias:{
		'vue$':'vue/dist/vue.common.js'
	}

}



用来在webpack中打包css、vue文件(加载器)
css-loader、:用于解决css调用引入问题
vue-loader
file-loader:用于处理css链入的外部文件处理
url-loader:在file-loader的基础上进行了扩展,增加了文件转化base编码功能


## webpack.config配置

```javascript
module.exports={
	entry:'',
	output:{},
	module:{},
	plugins:[]
};
```

### entry

注意事项：
- 1. entry参数：配置入口文件参数，可以放多入口文件
- 1. 一般将源文件放在src文件夹中

entry:"./a.js"						:把当前目录下的a.js打包成bundle.js,打包入口文件，一定要写好相对路径，不能直接写文件名
entry:["./src/a.js","./src/b.js"]	:这里表示有一个出口文件，并且这个文件对应两个js文件(多文件入口，单文件出口)
entry:{		
	output1:'./src/a.js',
	output2:['./src/b.js','./src/c.js']
},

### output								
output:{							:这里指产生两个出口文件，并且对应了(多文件入口多文件出口)
	filename:'[name].js',
	path:__dirname+'/dist'
}
filename		：表示对应的出口文件名，不输入文件名默认为哈希值,'[name].js]'表示以源文件名进行输出(如果是多文件入口是，并且给文件对应加了名字，最终就是在入口文件设置的名字)
path			：表示输出的文件存放的位置,这个路径的位置


#### path
path文件夹的位置确定的方式：
源文件中的路径是:'../images/big.jpg'

- 最后生成的路径是:'images/big.jpg'
- filel-loader在解析生成url路径时，的参照路径是配置文件中的output中的path的值:'demo4/dist',最后生成了'demo4/images/big.jpg',demo4本身是根目录，把这个路径最终进行简化就是/images/big.jpg
- 
- 根据上面的原理我们按一下过程分布:
- 1.源文件中的路径是:'../images/big.jpg';
- 2.真正要使用的图在路径是:'/dist/images/big.jpg';
- 
- 3.从1.2我们可以知道,index.html中要使用图片路径应该是:'/dist/images/big.jpg';
- 4.综上参考路径应该是'/dist/'
- 5.将file-loader的publicPath设为'./dist',表示告诉file-loader吧源文件中的路径中的相对定位入'../直接去掉，然后白身下的直接拼在一起./dist后面，就成了/dist/images/big.jpg'




### module
在module参数里面配置，webpack打包时候所需要的插件,每个加载的对象：第一个参数：配置要对什么类型的文件，第二个参数：用什么样的模块去加载
webpack1.x写法
loaders:[
	//当遇到文件名为.css结尾的文件去加载css-loader模块
	//管道pipe，从右往左执行对应的，将css-loader中的内容，通过style-loader将内容放到页面的style头部中
	{test:/\.css$/,loader:'style-loader!css-loader'},
],
webpack2.x写法
rules:[
	//数组写法也需要是pipe的写法
	{test:/\.css$/,use:['style-loader','css-loader']}
]

url-loader模块，比file-loader模块了一个base编码功能，可以设置大小，小于多少的变成base编码,减少请求数据
{
	test:/\.(gif|jpg|png|svg|jpe?g)$/,
	//loader:'file-loader?name=[name].[ext]&outPath=/images/'
	loader:'url-loader',
	options:{
		// 如果小于base64位编码，把图片变成base编码
		limit:8192,					
		//没有配置名字默认使用哈希值来命名、使用这种命名规范，打包成文件之后，采用以前的命名规则，name名字ext后缀名
		name:'[name].[ext]',
		//在输出之前，在这个文件名前面在加一个路径，用于区分文件存放
		outputPath:'/images/',
		// 此处要给相对于output配置的一个相对路径
		publicPath:'dist'
	}
},
上面的loader加载方式是以前的方法,新版方法

{

	test:/\.(gif|jpg|png|svg|jpe?g)$/,
	use:{
		loader:'url-loader',
		options:{
			limit:8192,
			name:'[name].[ext]',
		}
	}
}


### plugins

扩展插件使用:
plugins:[
	new webpack.optimize.UglifyJsPlugin({
		compress:{warnings:false}
	}),
	/*偷懒自动生成测试用html，而且这个html会自动应用我们生成的bundle.js文件*/
	new HtmlwebpackPlugin({title:'test'}),
	//热模块替换插件
	new webpack.HotModuleReplacementPlugin()
]

new webpack.optimize.UglifyJsPlugin：使用webpack里面自带的UglifyJs压缩插件，对文件进行压缩
这种使用情况需要导入webpack，才能使用

new UglifyJsPlugin({compress:{warning:false}})：单独下载了UglifyJsPlugin插件





HtmlwebpackPlugin:会将当前导出的所有文件路径引入到自动生成的一个html中，进行测试使用
引入:webpack-dev-server插件才能使用：
默认情况下不开启热替换(热替换的优势，在于对修改的内容进行替换，提高性能，不开启热替换，会全局替换，耗性能)
HotModuleReplacementPlugin:在修改文件之后，进行了保存操作，会触发保存在内存中，使用的数据，


启动webpack服务，可以将命令行保存在package.js中，使用npm run dev启动webpack-sev-server,并且开启一个express微型服务器，用来测试，当前的运行网站的状态

"build":"node_modules\\.bin\\webpack --watch",	启动webpack，并且实时监测当前文件的状态，如果发生改变就对导入的文件重新打包,监测除了webpack.config.js以外的文件
"dev":"node_modules\\.bin\\webpack-dev-server --inline"	启动webpack-dev-server,并实时监测当前文件的状态，如果发生改变就刷新服务器上的页面


## babel


rules{

	use:{
		test:/\.js$/,
		use:["babel-loader"],
		options:{
			
		}
		exclude:'/node_modules/'
	}
}