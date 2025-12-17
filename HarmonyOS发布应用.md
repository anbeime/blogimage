# 发布应用

更新时间: 2025-12-16 15:59

HarmonyOS通过数字证书与Profile文件等签名信息来保证应用/元服务的完整性，应用/元服务上架到AppGallery Connect必须通过签名校验。因此，您需要使用发布证书和Profile文件对应用/元服务进行签名后才能发布。

## 发布流程

开发者完成HarmonyOS应用/元服务开发后，需要将应用/元服务打包成App Pack（.app文件），用于上架到AppGallery Connect。发布应用/元服务的流程如下图所示：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155950.20219438340989908342964887364356:50001231000000:2800:3B4BE08A5657DEECFE0D763F75CDDEFA997E009C6993AFE4581CE40DE6A41EBD.png)

关于以上流程的详细介绍，请继续查阅本章节内容。

## 准备签名文件

HarmonyOS应用/元服务通过数字证书（.cer文件）和Profile文件（.p7b文件）来保证应用/元服务的完整性。在申请数字证书和Profile文件前，首先需要通过DevEco Studio来生成密钥（存储在格式为.p12的密钥库文件中）和证书请求文件（.csr文件）。

**基本概念**

- **密钥**：包含非对称加密中使用的公钥和私钥，存储在密钥库文件中，格式为.p12，公钥和私钥对用于数字签名和验证。
- **证书请求文件**：格式为.csr，全称为Certificate Signing Request，包含密钥对中的公钥和公共名称、组织名称、组织单位等信息，用于向AppGallery Connect申请数字证书。
- **数字证书**：格式为.cer，由华为AppGallery Connect颁发。
- **Profile文件**：格式为.p7b，包含HarmonyOS应用/元服务的包名、数字证书信息、描述应用/元服务允许申请的证书权限列表，以及允许应用/元服务调试的设备列表（如果应用/元服务类型为Release类型，则设备列表为空）等内容，每个应用/元服务包中均必须包含一个Profile文件。

### 生成密钥和证书请求文件

1. 在主菜单栏单击**Build > Generate Key** **and CSR**。
    
    说明
    
    如果本地已有对应的密钥，无需新生成密钥，可以在**Generate Key**界面中单击下方的Skip跳过密钥生成过程，直接使用已有密钥生成证书请求文件。
    
2. 在**Key Store File**中，可以单击**Choose Existing**选择已有的密钥库文件（存储有密钥的.p12文件）；如果没有密钥库文件，单击**New**进行创建。下面以新创建密钥库文件为例进行说明。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155950.59501853010631996107148716232278:50001231000000:2800:5746A95618BDEF616812E2FB601A5DD24B2430AB74090BDDFFA02FACEE026DCB.png "点击放大")
    
3. 在**Create Key Store**窗口中，填写密钥库信息后，单击**OK**。
    
    - **Key Store File**：设置密钥库文件存储路径，并填写p12文件名。
    - **Password**：设置密钥库密码，必须由大写字母、小写字母、数字和特殊符号中的两种以上字符的组合，长度至少为8位。请记住该密码，后续签名配置需要使用。
    - **Confirm Password**：再次输入密钥库密码。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155950.31030433422000605622389884256688:50001231000000:2800:EC2ADE92B7849411D7D7E8E166920276B1822E3E25D7953B4B0DC2FDD9AC7545.png "点击放大")
    
4. 在**Generate Key** **and CSR**界面中，继续填写密钥信息后，单击**Next**。
    
    - **Alias**：密钥的别名信息，用于标识密钥名称。请记住该别名，后续签名配置需要使用。
    - **Password**：密钥对应的密码，与密钥库密码保持一致，无需手动输入。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155950.42391649286372549798061239056702:50001231000000:2800:01663C0A41F2C5B15BED33ADC46713237C83A1B4D310BCAB94EF2230B6CB30C5.png)
    
5. 在**Generate Key** **and CSR**界面，设置CSR文件存储路径和CSR文件名。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155950.23528699079260975645090766360022:50001231000000:2800:B628D6D191DB217EE40BD1D59EFCA92BFAB686CDD6DC2AE78F1878E650D7B30C.png "点击放大")
    
6. 单击**OK**按钮，创建CSR文件成功，可以在存储路径下获取生成的密钥库文件（.p12）和证书请求文件（.csr）。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155950.37441664813745484212173196909014:50001231000000:2800:A00881A7D7A44CDC8C2310B11962606C8A1657675F48FBD3CAD88B715B7545B4.png)
    

### 申请发布证书和Profile文件

通过生成的证书请求文件，向AppGallery Connect申请发布证书和Profile文件，操作如下。

- 创建HarmonyOS应用/元服务：在AppGallery Connect项目中，创建一个HarmonyOS应用/元服务，用于发布证书和Profile文件申请，具体请参考[创建HarmonyOS应用](https://developer.huawei.com/consumer/cn/doc/app/agc-help-create-app-0000002247955506)和[创建元服务](https://developer.huawei.com/consumer/cn/doc/app/agc-help-create-atomic-service-0000002247795706)。
    
    说明
    
    如果申请元服务的签名证书，在“创建应用”操作时，“是否元服务”选项请选择“**是**”。
    
- 申请发布证书和Profile文件：在AppGallery Connect中申请、下载发布证书和Profile文件，具体请参考[申请发布证书](https://developer.huawei.com/consumer/cn/doc/app/agc-help-release-cert-0000002283336729)和[申请发布Profile](https://developer.huawei.com/consumer/cn/doc/app/agc-help-release-profile-0000002248341090)。

用于发布的证书和Profile文件申请完成后，请在DevEco Studio中进行签名，请参考[配置签名信息](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-publish-app#section280162182818)。

说明

使用发布证书和发布Profile文件进行手动签名，只能用来打包应用上架，不能用来运行调试工程。

## 配置签名信息

使用制作的私钥（.p12）文件、在AppGallery Connect中申请的证书（.cer）文件和Profile（.p7b）文件，在DevEco Studio配置工程的签名信息，构建携带发布签名信息的APP。

在**File >** **Project Structure >** **Project > Signing Configs** **> default**界面中，取消勾选“Automatically generate signature”和“Associate with registered application”，然后配置工程的签名信息。

- **Store File**：选择密钥库文件，文件后缀为.p12。
- **Store Password**：输入密钥库密码。
- **Key Alias**：输入密钥的别名信息。
- **Key Password**：输入密钥的密码。
- **Sign Alg**：签名算法，固定为SHA256withECDSA。
- **Profile File**：选择申请的发布Profile文件，文件后缀为.p7b。
- **Certpath File**：选择申请的发布数字证书文件，文件后缀为.cer。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155950.03612676116047764627907520808061:50001231000000:2800:6A3F91800FA31A8A14721A6886BC9092B1C1178A4629680D1F8DEDB4AB941590.png "点击放大")

设置完签名信息后，单击**OK**进行保存，然后使用DevEco Studio生成APP，请参考[编译构建.app文件](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-publish-app#section1992513343374)。

## （条件必选）更新公钥指纹

当应用需要使用以下开放能力的一种或多种时，发布应用前，需在[AppGallery Connect](https://developer.huawei.com/consumer/cn/service/josp/agc/index.html)中将调试应用的指纹更新为发布证书指纹。具体操作请参见[配置公钥指纹](https://developer.huawei.com/consumer/cn/doc/app/agc-help-cert-fingerprint-0000002278002933)。

- Account Kit（华为账号服务）
- Game Service Kit（游戏服务）
- Health Service Kit（运动健康服务）
- IAP Kit（应用内支付服务）
- Map Kit（地图服务）
- Payment Kit（华为支付服务）
- Wallet Kit（钱包服务）

## 编译构建.app文件

注意

应用上架时，要求应用包类型为Release类型。

打包APP时，DevEco Studio会将工程目录下的所有HAP/HSP模块打包到APP中，因此，如果工程目录中存在不需要打包到APP的HAP/HSP模块，请手动删除后再进行编译构建生成APP。

1. 单击**Build > Build Hap(s)/APP(s) > Build APP(s)**，等待编译构建完成已签名的应用包。
    
    说明
    
    当未指定[构建模式](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-compilation-options-customizing-guide#section192461528194916)时，构建APP包，默认Release模式；构建HAP/HSP/HAR包，默认Debug模式。
    
    即**Build APP(s)**时，默认构建的APP包为Release类型，符合上架要求，开发者无需进行另外设置。
    
2. 编译构建完成后，可以在工程目录**build > outputs > default**下，获取带签名的应用包。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155951.40649512218923781397010262426266:50001231000000:2800:2AE7D6ADC33AD50F66827482B08D29FF41E9498681EB20FF2072CF590EDE57AF.png)
    

## 上传软件包

DevEco Studio 5.0.5.200版本开始，支持在DevEco Studio内上传应用软件包。上传软件包前，请先[创建应用](https://developer.huawei.com/consumer/cn/doc/app/agc-help-create-app-0000002247955506)。

### 约束与限制

- 该功能仅支持中国境内（香港特别行政区、澳门特别行政区、中国台湾除外）。
- 该功能将会把您的应用包传至App Gallery Connect用于测试或上架。为了您的信息安全，请勿上传带有个人敏感信息的数据（如密码、源代码、私钥、调试安装包、业务日志等信息）。
- 仅Build Mode为Release的应用支持上传软件包，且确保软件包已配置Release签名。
- 同时支持通过[App Gallery Connect上传软件包](https://developer.huawei.com/consumer/cn/doc/app/agc-help-release-app-upload-pkg-0000002277983368)。

### 操作步骤

1. 在DevEco Studio菜单栏，点击**Build > Upload Product**，点击**Sign in**登录华为开发者账号。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155951.68478024841488056838337509964932:50001231000000:2800:BAF3E42C6005D733B26C4B407453156BDC70FB3342AB6A3D266986B0871F870B.png "点击放大")
    
2. 登录成功后，返回DevEco Studio进入软件包上传界面。确认当前工程的product信息，选择需要上传的软件包类型，点击OK开始上传。
    
    - 若当前上传的软件包仅做测试发布，请选择**Generate app package and upload it to AppGallery Connect for test**。
    - 若软件包需要在全网正式发布，请选择**Generate app package and upload it to AppGallery Connect for test and publish**。
    
    说明
    
    - 如需上传符号表信息，请勾选**Upload your app's symbols**选项。
    - 上传的product可以通过点击DevEco Studio编辑区域右上方![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155951.01935354391878553953635137338440:50001231000000:2800:99001E52C8CB6719E5B082D629CABD7DF3D1A6668681412DB0D21C130425729A.png)图标进行查看及切换。
    - 可通过app.json5中bundleName/versionName字段修改当前product对应的包名/版本号信息。必须使用当前开发者账号下已在AppGallery注册且真实存在的包名。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155951.99675306858177141979181701036953:50001231000000:2800:4A5C9D72B1BB4D352B739A0D69446D4A115C7E150B8BFE7E45A19449A09E6B64.png)
    
3. 上传完成后，出现云测试的结果，点击**View Full result in AppGallery Connect**可进入AGC查看软件包上传记录和检测结果，具体请参考[上传软件包](https://developer.huawei.com/consumer/cn/doc/app/agc-help-release-app-upload-pkg-0000002277983368)。点击**Close**关闭上传页面。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155951.03431851969869448313270780320403:50001231000000:2800:AFFF09F8676E7356BE6837365F9020CE3E000F6584AEAC4D7303B4558A9E227C.png)
    

## 发布.app文件到应用市场

将HarmonyOS应用/元服务打包成.app文件后上架到应用市场，发布详细操作指导请参考[发布HarmonyOS应用](https://developer.huawei.com/consumer/cn/doc/app/agc-help-release-app-0000002271695230)或[发布元服务](https://developer.huawei.com/consumer/cn/doc/app/agc-help-release-atomic-0000002327731065)。