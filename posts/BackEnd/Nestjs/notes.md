---
titleTemplate: Nestjs
---
# Nestjs学习记录

> 都说`Nestjs`好用，我也来浅学一下

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


