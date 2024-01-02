---


---

<p>@startuml</p>
<p>package “Frontend Application” {</p>
<p>[UI] as UI</p>
<p>[JavaScript] as JS</p>
<p>}</p>
<p>package “AWS Services” {</p>
<p>[Lambda Function] as Lambda</p>
<p>[Amazon Comprehend] as Comprehend</p>
<p>[Amazon S3] as S3</p>
<p>[Amazon CloudFront] as CloudFront</p>
<p>[API Gateway] as APIG</p>
<p>[Amazon Cognito] as Cognito</p>
<p>}</p>
<p>database “GPT-3” {</p>
<p>[Model] as GPT3</p>
<p>}</p>
<p>cloud “Google Translate API” {</p>
<p>[Translation Service] as Translate</p>
<p>}</p>
<p>UI -down-&gt; JS : User Interaction</p>
<p>JS -right-&gt; APIG : API Requests</p>
<p>APIG -down-&gt; Lambda : Triggers</p>
<p>Lambda -down-&gt; Comprehend : Extracts Keywords</p>
<p>Lambda -left-&gt; GPT3 : Generates Summary</p>
<p>Lambda -left-&gt; Translate : Translates Text</p>
<p>Cognito -up-&gt; JS : Manages Authentication</p>
<p>S3 -right-&gt; CloudFront : Hosts &amp; Distributes Web App</p>
<p>CloudFront -up-&gt; UI : Serves Web Pages</p>
<p>@enduml</p>
<p>@startuml</p>
<p>start</p>
<p>:User accesses the Web Application;</p>
<p>:User authenticates via Amazon Cognito;</p>
<p>if (Authenticated?) then (yes)</p>
<p>:User inputs document and selects language;</p>
<p>-&gt; API Gateway;</p>
<p>:API Gateway triggers Lambda Function;</p>
<p>:Lambda Function calls Amazon Comprehend;</p>
<p>split</p>
<p>:Extract Keywords from Document;</p>
<p>split again</p>
<p>:Generate Summary using GPT-3;</p>
<p>end split</p>
<p>:Translate Summary using Google Translate API;</p>
<p>:Return Translated Summary;</p>
<p>-&gt; API Gateway;</p>
<p>:Display Result in UI;</p>
<p>else (no)</p>
<p>:Redirect to Login;</p>
<p>endif</p>
<p>stop</p>
<p>@enduml</p>
<p>@startuml</p>
<p>actor “User” as user</p>
<p>participant “Frontend\nApplication” as frontend</p>
<p>database “Amazon\nCognito” as cognito</p>
<p>participant “API Gateway” as apigateway</p>
<p>participant “AWS Lambda\nand Other Services” as lambda</p>
<p>user -&gt; frontend : 输入邮箱和密码</p>
<p>frontend -&gt; cognito : 发送认证请求</p>
<p>cognito -&gt; cognito : 验证用户信息</p>
<p>alt 认证成功</p>
<p>cognito -&gt; frontend : 返回JWT令牌</p>
<p>frontend -&gt; user : 显示登录成功</p>
<p>user -&gt; frontend : 请求访问受保护的资源</p>
<p>frontend -&gt; apigateway : 使用JWT令牌调用API</p>
<p>apigateway -&gt; lambda : 触发Lambda函数</p>
<p>lambda -&gt; apigateway : 返回响应数据</p>
<p>apigateway -&gt; frontend : 转发响应</p>
<p>frontend -&gt; user : 展示数据</p>
<p>else 认证失败</p>
<p>cognito -&gt; frontend : 返回错误信息</p>
<p>frontend -&gt; user : 显示错误消息</p>
<p>end</p>
<p>@enduml</p>

