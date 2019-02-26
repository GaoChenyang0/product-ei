

# 1、参考文档

[通过身份服务器登录到wso2的产品](https://docs.wso2.com/display/IS570/Logging+in+to+WSO2+Products+via+the+Identity+Server)
# 2、操作步骤

## 2.1 规划IS身份服务器的域名:is.wc.mtn并配置身份服务器

* 打开<IS_HOME>\repository\carbon.xml文件，修改如下了个配置:

```xml
    <HostName>is.wc.mtn</HostName>
    <MgtHostName>is.wc.mtn</MgtHostName>
```
## 2.2 规划ei服务器的域名:bip.wc.mtn和bps.wc.mtn并配置sso

* 业务融合平台配置  打开<EI_HOME>\conf\carbon.xml文件，取消以下两个参数的注释并修改如下:

```xml
    <HostName>bip.wc.mtn</HostName>
    <MgtHostName>bip.wc.mtn</MgtHostName>
```
> 如果is服务器和ei服务器部署在同一台机器上，is服务器默认的端口偏移量(offset)为0，还需要在<EI_HOME>\conf\carbon.xml文件中修改ei服务器的端口偏移量(offset)为1

* 打开<EI_HOME>\conf\security\authenticators.xml文件，修改如下:

```xml
    <Authenticator name="SAML2SSOAuthenticator" disabled="false">
        <Priority>10</Priority>
        <Config>
            <Parameter name="LoginPage">/carbon/admin/login.jsp</Parameter>
            <Parameter name="ServiceProviderID">carbonServerEI</Parameter>
            <Parameter name="IdentityProviderSSOServiceURL">https://is.wc.mtn:9443/samlsso</Parameter>
            <Parameter name="NameIDPolicyFormat">urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified</Parameter>
            <Parameter name="AssertionConsumerServiceURL">https://bip.wc.mtn:9444/acs</Parameter>
```

* 流程整合平台配置  打开<EI_HOME>\wso2\business-process\conf\carbon.xml文件，取消以下两个参数的注释并修改如下:

```xml
    <HostName>bip.wc.mtn</HostName>
    <MgtHostName>bip.wc.mtn</MgtHostName>
```
> 如果is服务器和ei服务器部署在同一台机器上，is服务器默认的端口偏移量(offset)为0，还需要在<EI_HOME>\wso2\business-process\conf\carbon.xml文件中修改bps服务器的端口偏移量(offset)为2

* 打开<EI_HOME>\wso2\business-process\conf\security\authenticators.xml文件，修改如下:

```xml
    <Authenticator name="SAML2SSOAuthenticator" disabled="false">
        <Priority>10</Priority>
        <Config>
            <Parameter name="LoginPage">/carbon/admin/login.jsp</Parameter>
            <Parameter name="ServiceProviderID">carbonServerBPS</Parameter>
            <Parameter name="IdentityProviderSSOServiceURL">https://is.wc.mtn:9443/samlsso</Parameter>
            <Parameter name="NameIDPolicyFormat">urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified</Parameter>
            <Parameter name="AssertionConsumerServiceURL">https://bps.wc.mtn:9445/acs</Parameter>
```

## 2.3 在IS中添加并配置服务提供者carbonServerEI和carbonServerBPS
[通过身份服务器登录到wso2的产品](https://docs.wso2.com/display/IS570/Logging+in+to+WSO2+Products+via+the+Identity+Server)
## 2.4 测试SSO
[通过身份服务器登录到wso2的产品](https://docs.wso2.com/display/IS570/Logging+in+to+WSO2+Products+via+the+Identity+Server)

