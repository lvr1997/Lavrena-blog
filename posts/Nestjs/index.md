# Nestjs学习记录

> 都说`Nestjs`好用，我也来浅学一下

推荐入门文章

<Linkcard title="Vue3响应学完这篇 Nest.js 实战，还没入门的来锤我！" description="(长文预警)看到群里大家对`Nest.js`热情都很高,自己也心痒痒， - 掘金" url="https://juejin.cn/post/7032079740982788132?searchId=20240906140454C6682E9D087820816E35#heading-6" logo="https://lf-web-assets.juejin.cn/obj/juejin-web/xitu_juejin_web/static/favicons/favicon-32x32.png" />

## 有关Nestjs接口请求次数限制问题

Nestjs接口请求次数限制

```js
// app.module.ts 
import { APP_GUARD } from '@nestjs/core'; 
import { Module } from '@nestjs/common'; 
import { UserModule } from './modules/user/user.module'; 
//引入 
import { ThrottlerModule, ThrottlerGuard } from '@nestjs/throttler'; 

@Module({ 
	imports: [ 
		UserModule, 
		ThrottlerModule.forRoot({ 
			ttl: 60, //1分钟 
			limit: 10, //请求10次 
		}), 
	], 
	providers: [ 
	//全局使用 
	{ provide: APP_GUARD, useClass: ThrottlerGuard, }, 
	], 
}) 
export class AppModule { }
```

