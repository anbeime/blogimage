# 创建HarmonyOS应用工程

更新时间: 2025-12-16 15:57

## 新建工程

### 前提条件

- 您已使用[已实名认证](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-account)、且注册地为中国境内（香港特别行政区、澳门特别行政区、中国台湾除外）的华为开发者账号登录DevEco Studio。
- 请确保您的华为开发者账号无欠款，账户欠费将导致云存储服务开通失败。

### 选择模板

1. 选择以下任一种方式，打开工程创建向导界面。
    - 如果当前未打开任何工程，可以在DevEco Studio的欢迎页点击“Create Project”开始创建一个新工程。
    - 如果已经打开了工程，可以在菜单栏选择“File > New > Create Project”来创建一个新工程。
2. 在“Application”页签，选择合适的云开发模板，然后点击“Next”。
    
    说明
    
    当前仅支持通用云开发模板（[CloudDev]Empty Ability）。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155748.79600635581905896613258903958813:50001231000000:2800:95DE772A452C8FB4631AB532F0F6A6DBC3BA2E9B86B8D6182FF56F5D5846C7BA.png)
    

### 配置工程信息

1. 在工程配置界面，配置工程的基本信息。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155748.09106814919654489668258390741342:50001231000000:2800:EBFE43C0634201AC1682095F86B669C88F78DA160015D50A0DFE63D7E10CDF8B.png)
    
    |参数|说明|
    |:--|:--|
    |Project name|工程的名称，由大小写字母、数字和下划线组成。|
    |Bundle name|软件包名称，需保证唯一，且需与您在AGC创建的HarmonyOS应用的“应用包名”一致。|
    |Save location|工程文件本地存储路径，由大小写字母、数字和下划线等组成，不能包含中文字符。|
    |Compatible SDK|兼容的最低API Version。<br><br>使用基于Cloud Foundation Kit（云开发服务）的端云一体化开发功能，请选择5.0.0(12)或以上版本。|
    |Module name|模块名称。|
    |Device type|该工程模板支持的设备类型，目前仅支持手机设备。|
    |Enable CloudDev|是否启用云开发。云开发模板默认启用且无法更改。|
    

2. 点击“Next”，开始关联云开发资源。

### 关联云开发资源

为工程关联云开发所需的资源，即将您账号团队在AGC创建的同包名应用关联到当前工程。具体操作如下：

1. （可选）如您尚未登录DevEco Studio，点击“Sign In”，在弹出的账号登录页面，使用[已实名认证](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-account)的华为开发者账号完成登录。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155748.04968833567941547639261639896174:50001231000000:2800:3B49AA3789626A93139404F76A255137490DC11EB1899EA478AAFB232C1C5D13.png)
    
    登录成功后，界面将展示账号昵称。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155748.46252818223802355025715375411905:50001231000000:2800:6B854D119AB5347E14715735D49BCEDE5A5FCBB8C9B1867BEC0187413720CB2D.png)
    
2. 点击“Team”下拉框，选择开发团队。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155748.96784172007457244545840063411660:50001231000000:2800:7E573ACB3208A21C347C38E6B40BE531A568CCA3E87FA16527A9E27B4B4A27C9.png)
    
3. 关联应用。
    
    选中团队后，系统根据工程Bundle name在该团队中自动查询AGC上的同包名应用。
    
    - 如查询到应用，选中该应用，点击“Finish”即可。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155748.19778197266601023168405275463498:50001231000000:2800:78D25981863A478E2A21A3FA5CCB11AB2FEBBA90B71CB78A6D61395785BAB030.png)
        
    - 如查询到的应用尚未关联任何项目（即为游离应用），则无法选中。请先[将游离应用添加到AGC项目下](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-create-appproject#section152521927193013)。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155748.46645413620803103514499056286310:50001231000000:2800:4990DA48B7CBDC91FCEC9ABCFEC81366AAE6D86DA84A19D7BB47273AD0843C31.png)
        
    - 如果查询到的应用所属项目尚未启用数据处理位置，请点击界面提示内的“AppGallery Connect”[设置数据处理位置](https://developer.huawei.com/consumer/cn/doc/app/agc-help-datalocation-0000001160439813)。设置完成后返回DevEco Studio界面，点击Bundle name后的![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155748.22309878715300224231410186422492:50001231000000:2800:471CF7502E055FE04F6577FA8770D7BA9567C2F7FCF447ACA0FB0A69BC82508B.png)刷新当前APP ID列表，即可看到设置的数据处理位置。
        
        注意
        
        - 由于云开发目前仅支持中国站点，请确保项目启用的数据处理位置包含中国站点。
        - 无论项目启用的默认数据处理位置为哪个站点，后续开发的云服务资源都将部署在中国站点。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155748.90233515267212782252103874340610:50001231000000:2800:B96AD69DF9406CDE76113B4CF011EDE6C61211445884FAD996A4EA196EEB18E5.png)
        
    - 如查询到应用但出现如下提示，表明查询到的应用类型为元服务，与当前工程类型不一致。请修改以确保当前工程与AGC上同包名应用均为HarmonyOS应用类型。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155748.55527931854692162934025286125557:50001231000000:2800:74BD50732C6A0689DD5A920BF15E68F72B503F008D0009EECB936DA6257894F9.png)
        
    
    - 如在当前团队中未查询到同包名应用，请先确认填写的包名是否有误。
        
        - 如包名有误，点击界面提示中的“go back”返回工程信息配置界面进行修改。
        - 如包名无误，则表明当前团队尚未在AGC控制台创建与当前工程包名相同的应用。您可点击界面提示中的“AppGallery Connect”，[前往AGC控制台进行补充创建](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-create-appproject#section397317130308)。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155748.05745156566973796578653032830764:50001231000000:2800:0FBA31346FF14714DCD9610E99048B47122AE0964F76E88AA6B1FC260BE96062.png)
        
        完成以上操作后，DevEco Studio即可获取到同包名应用信息。选中应用后，点击“Finish”。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155748.62885876124172032709536547015914:50001231000000:2800:0A9FABB4E0FECC2C84B76F20EF0B2B2BFBBFA72A5AD742293E7E2ABFDDF3672A.png)
        
4. 如您所属的团队尚未签署云开发相关协议，点击协议链接仔细阅读协议内容后，勾选同意协议，点击“Finish”。
    
    说明
    
    只有账号持有者和法务角色才有权限签署协议。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155749.13185191075503770384826604850715:50001231000000:2800:2C8778746AEBEBF554E34854F1ED0A788843375BDAB3F8683E8232C62C55C247.png)
    
5. 进入主开发界面，DevEco Studio执行工程同步操作，端侧工程会自动执行“ohpm install”，云侧工程会自动执行“npm install”，以分别下载端侧和云侧依赖。
    
    说明
    
    若云侧执行“npm install”失败，请排查是否尚未[配置NPM代理](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-environment-config#section197296441787)。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155749.58025678440190351870759122932311:50001231000000:2800:188E35BC2A3EE957429152C1788DA057FE30404DBB2CDAC1EEFA1D9E8F8296C3.png)
    
6. 在主开发界面，可查看刚刚新建的工程。关于工程的详细目录结构介绍，请参见[端云一体化开发工程目录结构](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-create-appproject#section20250910164411)。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155749.89984585890931198496864436717181:50001231000000:2800:E6D59C1A429CDF1D6E8B0B6321D1D3819884810AADC7073143ACE791768931C0.png)
    

## 工程初始化配置

当您成功创建工程并关联云开发资源后，DevEco Studio会为您的工程自动执行一些初始化配置。

### 自动开通云开发服务

DevEco Studio为工程关联的项目自动开通云函数、云数据库、云存储等云开发服务，您可在“Notifications”窗口查看服务开通状态。

说明

- 如服务开通失败，您可通过[CloudDev云开发管理面板](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-console)快捷进入AGC控制台进行手动开通。
- 如云存储服务自动开通与手动开通均失败，可能是账户欠费导致。请您[检查账户是否余额不足](https://developer.huawei.com/consumer/cn/doc/AppGallery-connect-Guides/agc-account-bill-0000001200817917#section813072912208)，[补齐欠款](https://developer.huawei.com/consumer/cn/doc/AppGallery-connect-Guides/agc-account-recharge-0000001126625360)后再前往AGC控制台进行手动开通。

## 端云一体化开发工程目录结构

端云一体化开发工程主要包含端开发工程（Application）与云开发工程（CloudProgram）。

### 端开发工程（Application）

端开发工程主要用于开发应用端侧的业务代码，通用云开发模板的端开发工程目录结构如下图所示。“Application/cloud_objects”模块用于存放云对象的端侧调用接口类，“src/main/ets/pages”目录下包含了云存储、云数据库和云函数页面，其他目录文件介绍请参见[工程目录结构](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-project-structure)。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155749.26739765724565654296781574654314:50001231000000:2800:43162DD3B3EE4CFAC8B3CE0BA64FD3DABBF892A3BED73DBB65A0B1B96C211FC0.png)

### 云开发工程（CloudProgram）

在云开发工程中，您可为您的应用开发云端代码，包括云函数和云数据库服务代码。通用云开发模板的云开发工程目录结构如下图所示。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155749.05554049389182174904484470665450:50001231000000:2800:8A9EAD8469959C85C53417F9985F4C139FBED37CCFC05F633FC7738E75DAC7F2.png)

- clouddb：云数据库目录，包含数据条目目录（dataentry）和对象类型目录（objecttype）。
    - dataentry：用于存放数据条目文件。
        
        该目录下一般会根据您选择的云开发模板预置数据条目示例文件。在通用云开发模板工程中，该目录下会预置名为“d_Post.json”的数据条目示例文件，内含两条示例数据。您可按需使用、修改或删除。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155749.65818031514088143696980910099302:50001231000000:2800:8FF22149FABAC3385899FD212897E8B1AF59502FF5214FA9FC8365238024BEF8.png)
        
    - objecttype：用于存放对象类型文件。
        
        该目录下一般会根据您选择的云开发模板预置对象类型示例文件。在通用云开发模板工程中，该目录下会预置名为“Post.json”的对象类型示例文件，内含对象类型“Post”的权限、索引、字段名称和字段值等。您可按需使用、修改或删除。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155749.11060082129160393148411388468060:50001231000000:2800:A33CEBE43B7B848DD253BD2F94F14CE03F9C7514BCBB4560C68AF82D59B9D555.png)
        
    - db-config.json：模块配置文件，主要包含云数据库工程的配置信息，如默认存储区名称、默认数据处理位置。
- cloudfunctions：云函数目录，包含各个云函数/云对象子目录。每个子目录下包含了云函数/云对象的配置文件、入口文件、依赖文件等。
    
    该目录下一般会根据您选择的云开发模板预置示例函数。通用云开发模板工程下预置了一个用于生成UUID的示例云对象“id-generator”，您可按需使用、修改或删除。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155749.94293990687352680285306043751250:50001231000000:2800:A6C9681DE53425D4D0F2EEFEF99DDB5AE26955C8B3B3C9168A9079ED933A50A5.png)
    
- node_modules：工程同步时执行“npm install”生成，包含“typescript”和“@types/node”公共依赖。
- cloud-config.json：云开发工程配置文件，包含应用名称与ID、项目名称与ID、启用的数据处理位置、支持的设备类型等。
- package.json：定义了“typescript”和“@types/node”公共依赖。
- package-lock.json：工程同步时执行“npm install”生成，记录当前状态下实际安装的各个npm package的具体来源和版本号。

## （可选）AGC应用管理

### 从DevEco Studio补充创建同包名应用

如创建工程时，发现尚未在AGC控制台创建与工程包名相同的应用，可进行补充创建。

1. 点击界面提示内的“AppGallery Connect”，浏览器打开AGC控制台页面。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155749.91654240188293103973679882255946:50001231000000:2800:4F4360EAF12E4537AEDF50A35272952C8EE1725BE5051E9AD9AAB5F583AE3668.png)
    
2. 在“应用开发基础信息”页面，填写待创建的应用信息，完成后点击“下一步”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155749.00426337137573088170794093654724:50001231000000:2800:FE52BF21C23FC4C2EAC3501A654B47128478161742B35B7FF324FB55B76D71E5.png)
    
    |参数|说明|
    |:--|:--|
    |应用类型|创建的HarmonyOS应用形态，默认与您本地工程类型保持一致，不可更改。|
    |应用名称|应用在华为应用市场详情页展示的名称。|
    |应用包名|从DevEco Studio中带入自动填充，且不可更改。|
    |应用分类|请选择普通应用或游戏类应用。<br><br>说明<br><br>应用分类设置后不支持修改，请谨慎选择。|
    
3. 进入“所属项目信息”页面，为应用选择所属的项目后点击“下一步”。
    
    - 如需将应用添加到已有项目，点击下拉框进行选择。
    - 如需将应用添加到新项目，直接在框中填写新项目名称。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155749.09403337511118861079209499164839:50001231000000:2800:BBC309EB22F7C72916F61F4697CDF5F404EE493721B39587B6186DBD00586BC3.png)
    
4. 进入“云开发数据处理位置”页面，设置或管理项目的数据处理位置。
    - 如项目尚未设置数据处理位置：
        1. 点击“启用”。
            
            ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155749.25887511605284306915318961641732:50001231000000:2800:9AD9BA6F72E7849FB557078C242DC7507C3EE1CC08FB1B158BE995CEDF2FE610.png)
            
        2. 仔细阅读提示框的文字说明后，在“启用”栏为您的项目勾选一个或多个数据处理位置，并在“设为默认”栏将其中一个设置为默认数据处理位置。
            
            注意
            
            启用的数据处理位置必须包含中国站点。
            
            ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155749.48953691115978972873506320144540:50001231000000:2800:4BB6BA477D5E9AEA5928E399B23AE2E925812975F45950EB66F9789E54F4DBC2.png)
            
    - 如项目已设置过数据处理位置，可点击“管理”启用新的数据处理位置、取消已启用的数据处理位置，或修改默认数据处理位置。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155749.35634169834506782786978179773238:50001231000000:2800:3C71FBDB534675BC8DE4973C69F0CD6B76BCA50636657E2BECDC124DF82CA832.png)
        
5. 点击“确认”，应用创建完成。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155749.99694691054037837303988949035666:50001231000000:2800:7DF8A60710B2514372392D89662C726274FD3D557D32728C9E03C593A3CCDBAA.png)
    
6. 返回DevEco Studio，可看到界面已获取并展示了刚刚创建的应用信息。若不展示，可点击Bundle name后的![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155749.95422172943089818171874434273892:50001231000000:2800:683F26075DF47B3CBD6B260012787A41E7494869BA6BAA801689DD7CF111D8B7.png)刷新。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155750.82285921831418952191230390269815:50001231000000:2800:F8476950293750DE9E727E15D5EA26B906CDEBB30D236521864376985421A6DE.png)
    

### 将游离应用添加到AGC项目下

游离应用指未关联任何AGC项目的应用。创建工程时，如需要关联的AGC应用为游离应用，则您需要将该应用添加到您的AGC项目下。

注意

应用与项目的关联关系一旦创建则无法再修改，请谨慎操作。

1. 点击“Not associated yet”，或点击界面下方提示内的“AppGallery Connect”，可打开AGC控制台“开发与服务”页面。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155750.60903032257795107976231438694545:50001231000000:2800:1E626ABC0ADCAD6261292E934A2B9654D662823A9BCB058303576429BDBCF5C6.png)
    
2. 点击选择希望为应用关联的项目，或者点击“添加项目”新建一个项目。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155750.04809654818357657037847163127416:50001231000000:2800:E181237385E3F2660513BD2C5E6D5C16A4970772E667D7204981C159124C2262.png)
    
3. 如选择了新建一个项目，设置项目名称，点击“确认”。
    
    如选择了已有项目，则忽略此步骤。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155750.64953810466875571569545453711725:50001231000000:2800:B72CE5D4FBC2B160AA3FA773BBD9DB1EF6205B0C5D7B9D57E3476677BF38B35A.png)
    
4. 设置或管理项目的数据处理位置。
    - 如项目尚未设置数据处理位置：
        1. 点击“启用”。
            
            ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155750.23579299828330905476898557230758:50001231000000:2800:0E99B95B084F396D4F458C06C4DC57AB2B8D93DA70D785CD3D3324964EF0867F.png)
            
        2. 仔细阅读提示框的文字说明后，在“启用”栏为您的项目勾选一个或多个数据处理位置，并在“设为默认”栏将其中一个设置为默认数据处理位置。
            
            注意
            
            启用的数据处理位置必须包含中国站点。
            
            ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155750.14842160459851708955058791692846:50001231000000:2800:7BE29341F8469394830FF2BC81C6999D99D5C67FF99E8DD2E5920EE65F66D992.png)
            
    - 如项目已设置过数据处理位置，可点击“管理”启用新的数据处理位置、取消已启用的数据处理位置，或修改默认数据处理位置。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155750.68408943126992713958694126826552:50001231000000:2800:D06C4AF820EA79043336008AAF4274F559FE191C8C535C9DFE14E1879E313732.png)
        
5. 点击“确认”，应用成功关联项目。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155750.82760883425287818385889458424475:50001231000000:2800:A6D0CE1FFA2A6BB0E77E02BFAEDABCE3934E46D1C46253DC208D6AD3E1E07D60.png)
    
6. 返回DevEco Studio，可看到应用已关联上了项目。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155750.36920958218481230619902061616431:50001231000000:2800:5ED9657F8C38FCCDA2D85F20658CE35E061EA431659AD5472E7DC2FE9A121790.png)
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-devproject "创建端云一体化开发工程")
# 创建元服务工程

更新时间: 2025-12-16 15:57

## 新建工程

### 前提条件

- 您已使用[已实名认证](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-account)、且注册地为中国境内（香港特别行政区、澳门特别行政区、中国台湾除外）的华为开发者账号登录DevEco Studio。
- 请确保您的华为开发者账号无欠款，账户欠费将导致云存储服务开通失败。

### 选择模板

1. 选择以下任一种方式，打开工程创建向导界面。
    - 如果当前未打开任何工程，可以在DevEco Studio的欢迎页点击“Create Project”开始创建一个新工程。
    - 如果已经打开了工程，可以在菜单栏选择“File > New > Create Project”来创建一个新工程。
2. 点击“Atomic Service”页签，选择合适的云开发模板，然后点击“Next”。
    
    说明
    
    当前仅支持通用云开发模板（[CloudDev]Empty Ability）。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155752.22049203275612152534644681538035:50001231000000:2800:695AF3FB8C175A0DF39EEFD1A3E0FE08D64D9312A63766D6A2B5A31FFD8C5458.png)
    

### 关联云开发资源

为工程关联云开发所需的资源，即将您账号团队在AGC创建的元服务关联到待创建工程。具体操作如下：

1. （可选）如您尚未登录DevEco Studio，点击“Sign In”，在弹出的账号登录页面，使用[已实名认证](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-account)的华为开发者账号完成登录。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155752.92761315675236902163777029122570:50001231000000:2800:F23E87676666C6986D3237850913E45574A644C6AD49A8664B32C373A4971857.png)
    
    登录成功后，界面将展示账号昵称。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155752.45154794798658751641474045503488:50001231000000:2800:42D2D0A76098993EAF00C7AB216E30C502D55DE08DA6DDDEAEF48E62C85E4137.png)
    
2. 选择已登录账号下的APP ID，以关联AGC上的元服务。
    
    - 从APP ID下拉列表中选中所需的APP ID后，界面会展示该元服务在AGC控制台的名称、所属项目、包名与数据处理位置。确认无误后，点击“Next”。
        
        说明
        
        元服务包名为自动生成，格式为固定前缀与appid的组合（com.atomicservice.[appid]）。不符合命名规范的包名无法在APP ID下拉列表中展示。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155752.97315914944044832088405602764847:50001231000000:2800:2E44F014E140AF940239BCF8744B0856CA92FF900ECB116E64E4D1C0FCD2E270.png)
        
    
    - 当出现以下场景时，您可点击“Register App ID”，[前往AGC控制台补充创建元服务](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-create-faproject#section397317130308)。创建成功后返回DevEco Studio界面，即可看到新建的元服务信息。
        
        - APP ID框为空，即当前账号尚未在AGC控制台创建任何元服务。
        - 您需为待创建工程关联一个新的元服务。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155752.82880155826175568318779981700426:50001231000000:2800:1E7252437144E9ACEDCCD3BBC200C9E1D6E1A2CB875E8226EBE78DD17C2DD821.png)
        
    - 如查询到的元服务尚未关联任何项目，则无法选中。请先[将游离元服务添加到AGC项目下](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-create-faproject#section152521927193013)，再返回DevEco Studio界面操作。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155752.26521933433004547871190043743385:50001231000000:2800:EEF60534713D0A6BC57EEE7E8F2F5222C9FD7A695D6FAAA0BCC86ACCA6076F1D.png)
        
    
    - 如果查询到的元服务所属项目尚未启用数据处理位置，请点击界面提示内的“AppGallery Connect”[设置数据处理位置](https://developer.huawei.com/consumer/cn/doc/app/agc-help-datalocation-0000001160439813)。设置完成后返回DevEco Studio界面，点击“Refresh”刷新当前APP ID列表，即可看到设置的数据处理位置。
        
        注意
        
        - 由于云开发目前仅支持中国站点，请确保项目启用的数据处理位置包含中国站点。
        - 无论项目启用的默认数据处理位置为哪个站点，后续开发的云服务资源都将部署在中国站点。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155752.74609894718131148022707359392380:50001231000000:2800:A6F692650FC33CBBE6765A17940890CAAB2F61EC51DD0E3F840E1626D529E916.png)
        
    

### 配置工程信息

1. 进入工程配置界面，配置工程的基本信息。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155752.23185552798255858351829252801055:50001231000000:2800:930B47772B47E6F1C1D9B251DCB098EE7009543542073C81A061BE9CCC622C44.png)
    
    |参数|说明|
    |:--|:--|
    |Project name|工程的名称，由大小写字母、数字和下划线组成。|
    |Bundle name|创建元服务时自动生成，不支持手动修改。|
    |Save location|工程文件本地存储路径，由大小写字母、数字和下划线等组成，不能包含中文字符。|
    |Compatible SDK|兼容的最低API Version。<br><br>元服务使用基于Cloud Foundation Kit（云开发服务）的端云一体化开发功能，请选择5.0.0(12)或以上版本。|
    |Module name|模块名称。|
    |Device type|该工程模板支持的设备类型，目前仅支持手机设备。|
    |Enable CloudDev|是否启用云开发。云开发模板默认启用且无法更改。|
    

2. 点击“Finish”，进入主开发界面，DevEco Studio执行工程同步操作，端侧工程会自动执行“ohpm install”，云侧工程会自动执行“npm install”，以分别下载端侧和云侧依赖。
    
    说明
    
    若云侧执行“npm install”失败，请排查是否尚未[配置NPM代理](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-environment-config#section197296441787)。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155752.65085991566600370786968295906752:50001231000000:2800:75A1C9BAA2C791EA550DB16A9D90254C903C6CF026C2CD6365B5F800537AFB90.png)
    
3. 在主开发界面，可查看刚刚新建的工程。关于工程的详细目录结构介绍，请参见[端云一体化开发工程目录结构](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-create-faproject#section20250910164411)。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155752.47619446026878472776362751035481:50001231000000:2800:687DB46B8AD36B59CEBBEFFD6A2E69D3678A49F974CE8CCA40A05EF03BFB8FEC.png)
    

## 工程初始化配置

当您成功创建工程并关联云开发资源后，DevEco Studio会为您的工程自动执行一些初始化配置。

### 自动开通云开发服务

DevEco Studio为工程关联的项目自动开通云函数、云数据库、云存储等云开发服务，您可在“Notifications”窗口查看服务开通状态。

说明

- 如服务开通失败，您可通过[CloudDev云开发管理面板](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-console)快捷进入AGC控制台进行手动开通。
- 如云存储服务自动开通与手动开通均失败，可能是账户欠费导致。请您[检查账户是否余额不足](https://developer.huawei.com/consumer/cn/doc/AppGallery-connect-Guides/agc-account-bill-0000001200817917#section813072912208)，[补齐欠款](https://developer.huawei.com/consumer/cn/doc/AppGallery-connect-Guides/agc-account-recharge-0000001126625360)后再前往AGC控制台进行手动开通。

## 端云一体化开发工程目录结构

端云一体化开发工程主要包含端开发工程（Application）与云开发工程（CloudProgram）。

### 端开发工程（Application）

端开发工程主要用于开发应用端侧的业务代码，通用云开发模板的端开发工程目录结构如下图所示。“Application/cloud_objects”模块用于存放云对象的调用接口类，“src/main/ets/pages”目录下包含了云存储、云数据库和云函数页面，其他目录文件介绍请参见[工程目录结构](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-project-structure)。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155752.80520404672928882817424043447963:50001231000000:2800:2ECDCF6BBF64ED101C6E9B9C77DD2E046D4775DAB56B759FF62EB23CB4A4C77F.png)

### 云开发工程（CloudProgram）

在云开发工程中，您可为您的元服务开发云端代码，包括云函数和云数据库服务代码。通用云开发模板的云开发工程目录结构如下图所示。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155753.55033108513751341851344033240296:50001231000000:2800:F86A7DC7C6425D6406E8D546745944BDD3D20A2BFDF27CCA55066831CB5B1210.png)

- clouddb：云数据库目录，包含数据条目目录（dataentry）和对象类型目录（objecttype）。
    - dataentry：用于存放数据条目文件。
        
        该目录下一般会根据您选择的云开发模板预置数据条目示例文件。在通用云开发模板工程中，该目录下会预置名为“d_Post.json”的数据条目示例文件，内含两条示例数据。您可按需使用、修改或删除。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155753.44926810331125522865893627698957:50001231000000:2800:A31472FD0606DCABE293556840FECB761DDCC57CD525AD6C1DD97D3D20234874.png)
        
    - objecttype：用于存放对象类型文件。
        
        该目录下一般会根据您选择的云开发模板预置对象类型示例文件。在通用云开发模板工程中，该目录下会预置名为“Post.json”的对象类型示例文件，内含对象类型“Post”的权限、索引、字段名称和字段值等。您可按需使用、修改或删除。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155753.12545969390383319922372190934581:50001231000000:2800:F212DDA677E0C0F96EACBCDAD128B6AB4841F47EF30D8087E8E598989831FFFF.png)
        
    - db-config.json：模块配置文件，主要包含云数据库工程的配置信息，如默认存储区名称、默认数据处理位置。
- cloudfunctions：云函数目录，包含各个云函数/云对象子目录。每个子目录下包含了云函数/云对象的配置文件、入口文件、依赖文件等。
    
    该目录下一般会根据您选择的云开发模板预置示例函数。通用云开发模板工程下预置了一个用于生成UUID的示例云对象“id-generator”，您可按需使用、修改或删除。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155753.62959246847683245517044094369095:50001231000000:2800:5428E31DADE020FA6B7295666865A30D8C183438D0488FDD637B280EA4E8EEA9.png)
    
- node_modules：工程同步时执行“npm install”生成，包含“typescript”和“@types/node”公共依赖。
- cloud-config.json：云开发工程配置文件，包含应用名称与ID、项目名称与ID、启用的数据处理位置、支持的设备类型等。
- package.json：定义了“typescript”和“@types/node”公共依赖。
- package-lock.json：工程同步时执行“npm install”生成，记录当前状态下实际安装的各个npm package的具体来源和版本号。

## （可选）AGC元服务管理

### 从DevEco Studio补充创建元服务

如创建元服务工程时，发现尚未在AGC控制台创建对应的元服务，可直接从DevEco Studio进行补充创建。

1. 点击“Register App ID”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155753.07801216629980392786699126225209:50001231000000:2800:4B3871872FAB72879F6F3BEF3AB0C54C441F3CCDE8C9C78C588E57A24D1E234F.png)
    
2. 在弹窗中填写待创建的元服务信息后，点击“OK”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155753.21908308395150269028131723703753:50001231000000:2800:9692690C1552D80F47438F58FCAFDA64705AF397611034AA14491177A1D02758.png)
    
    |参数|说明|
    |:--|:--|
    |Project|为当前元服务选择所属的项目。可以输入一个新项目名称，或在下拉框中选择已有项目。|
    |App type|应用形态。默认为“AtomicService”，不支持修改。|
    |App name|元服务在华为应用市场详情页展示的名称。|
    |App category|应用分类。元服务暂不支持游戏类别，请选择“App”。<br><br>说明<br><br>应用分类设置后不支持修改，请谨慎选择。|
    
3. 返回DevEco Studio界面，可查看到刚刚创建的元服务的名称及APP ID、所属项目及项目ID、包名、数据处理位置。
    
    说明
    
    若元服务关联的是一个新建项目或者尚未启用数据处理位置的已有项目，则还会提示尚未启用数据处理位置，参考[上文](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-create-faproject#li58931263712)处理即可。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155753.63829788964561050764731113453302:50001231000000:2800:43D0494BF2A3BBF627E6C595DC4BC7D808A8FA083CE2ECADD89EDC26FF146F4B.png)
    

### 将游离元服务添加到AGC项目下

游离元服务指未关联任何AGC项目的元服务。创建工程时，如需要关联的AGC元服务为游离状态，则您需要将该元服务添加到您的AGC项目下。

注意

元服务与项目的关联关系一旦创建则无法再修改，请谨慎操作。

1. 点击“Not associated yet”，或点击界面下方提示内的“AppGallery Connect”，可打开AGC控制台“开发与服务”页面。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155753.07606077430602321534420774081240:50001231000000:2800:510B74EC2E5A5884BF36427B7B4486776EA490813802AB8D5BEF4142A4271DA6.png)
    
2. 点击选择希望为元服务关联的项目，或者点击“添加项目”新建一个项目。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155753.22972333898490651116792084138821:50001231000000:2800:445E41C9CD31535F9FA612BB726BD88124CC37ED4F839A7E608FD207CDAB165B.png)
    
3. 如选择了新建一个项目，设置项目名称，点击“确认”。
    
    如选择了已有项目，则忽略此步骤。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155753.82178835541070298312572301625007:50001231000000:2800:D7967D9E2C35877CE602F2C45163A547666528DD4786764CE23F82B1DDEC1A78.png)
    
4. 设置或管理项目的数据处理位置。
    - 如项目尚未设置数据处理位置：
        1. 点击“启用”。
            
            ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155753.39145209084376842144268631936797:50001231000000:2800:23A8329516193133447C1D01C19219ADC6F7245D55C161BB6DAE6E59E74A7D9D.png)
            
        2. 仔细阅读提示框的文字说明后，在“启用”栏为您的项目勾选一个或多个数据处理位置，并在“设为默认”栏将其中一个设置为默认数据处理位置。
            
            注意
            
            启用的数据处理位置必须包含中国站点。
            
            ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155753.81543814712950213615276392596579:50001231000000:2800:13808F0594397948E2A71EE8ED9CF78A69C3E9B1AEA64B918D5069AB2E2C0F20.png)
            
    - 如项目已设置过数据处理位置，可点击“管理”启用新的数据处理位置、取消已启用的数据处理位置，或修改默认数据处理位置。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155753.75789320553542914779058627808349:50001231000000:2800:C4F0196F40C10B6D4C13E93E7DDF5A37544CE31D238C20151C7F76B1890A9B03.png)
        
5. 点击“确认”，元服务成功关联项目。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155753.98258676870375502987915990320492:50001231000000:2800:FD1E3B90DCBE846031778B938CB5040FD97FA0BEA6C56A9CBA73D8AA70071B0D.png)
    
6. 返回DevEco Studio，点击“Refresh”刷新，可看到元服务已关联上了项目。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155753.13281887693946892547573538673065:50001231000000:2800:32C7C2A7C8DDD4E7D6296A57E61A4D7FCD8ECDB07B96D87EA985DB9BE6CD19FA.png)
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-create-appproject "创建HarmonyOS应用工程")
# 历史工程转换为端云一体化开发工程

更新时间: 2025-12-16 15:57

如您此前已经创建了非端云一体化开发工程，希望直接转换为端云一体化开发工程，可执行如下操作：

说明

DevEco Studio NEXT Beta1版本之前的非端云一体化历史工程，在转换前需先进行[一体化工程迁移](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V14/ide-integrated-project-migration-V14)。

1. [创建一个端云一体化开发工程](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-devproject)，其中工程的类型（HarmonyOS应用或元服务）必须与您历史工程类型一致，同时Bundle name必须指定为您历史工程的Bundle name。在创建端云一体化开发工程过程中，该Bundle name会关联到AGC应用、项目等云端资源。
2. 打开创建的端云一体化开发工程，右击端开发工程“Application”，选择“Open In > Explorer”，打开工程文件所在的目录。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155754.72114179069147137584679119664436:50001231000000:2800:AE33EA07BB739C5FBBE06BACF6E55B212E2B4C61CC5F2F37D4F98886B8591A7D.png)
    
3. 删除端云一体化开发工程的端侧工程目录“Application”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155754.17662145483806537855478340885019:50001231000000:2800:45920C1454202E4B20144FD9373A6A4746B96DD75AF7CC70462B87C33C400C62.png)
    
4. 将历史工程目录（如“MyApplication30”）拷贝至[步骤3](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-project-migration#li104559101267)的端云一体化开发工程目录下，并改名为“Application”。
5. 重新打开端云一体化开发工程，可发现历史工程的端侧代码已迁移至端云一体化开发工程。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-create-faproject "创建元服务工程")
# 开发流程

更新时间: 2025-12-16 15:57

云函数是一项Serverless计算服务，可以根据函数的实际流量对函数进行弹性收缩。您只需聚焦业务逻辑，开发与上传业务模块相关的函数，云函数即可为您自动完成资源分配、代码部署、负载均衡等工作，既提高了开发和上线函数的速度，也保证了函数的高可用性。

云函数当前分为传统云函数和云对象两种类型，本章节仅介绍传统云函数，了解云对象详情请参考[开发云对象](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-cloudobj)。

使用DevEco Studio在端云一体化云侧工程下开发云函数，总体流程如下。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155754.65568840935962363876448632076344:50001231000000:2800:81018B6177A41C46652260A5B47468991F983FA30880A8B7871DE6C4E2561AD4.png "点击放大")

1. [创建并配置函数](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-createfunc)：您可直接在DevEco Studio创建函数、为函数配置入口以及调用的触发器等。
2. [开发函数](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-funccoding)：函数创建并配置完成后，您便可以开始编写函数业务代码了。
3. [调试函数](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-debugfunc)：您可以对函数进行调试，以测试函数代码运行是否正常。
4. [部署函数](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-deployfunc)：完成函数代码开发与调试后，您可将函数部署到AGC云端，支持单个部署和批量部署。

说明

一般建议先将函数调试无误后再部署至云端，但某些业务场景下需要先部署函数才能进行调试。请根据实际业务需要操作。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-cloudfunctions "开发云函数")
# 创建并配置函数

更新时间: 2025-12-16 15:57

您可直接在DevEco Studio创建函数、为函数配置调用的触发器等。

## 创建函数

1. 右击“cloudfunctions”目录，选择“New > Cloud Function”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155755.10559866167505149469186875889865:50001231000000:2800:E95182784612EDF6ED6CD7B644DB01A9A6114EF8C377ED8126DD74798635ABE6.png)
    
2. 在“Select the Cloud Function Type”栏选择“Cloud Function”，输入云函数名称（如“my-cloud-function”），点击“OK”。
    
    函数名称长度2-63个字符，仅支持小写英文字母、数字、中划线（-），首字符必须为小写字母，结尾不能为中划线（-）。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155755.86573017809628721735664219850360:50001231000000:2800:5D50510CE9755514D992F7598432ED186760C87B6CC2ED3D19C7C16598FB4FF1.png)
    
    “cloudfunctions”目录下生成新建的“my-cloud-function”函数目录，目录下主要包含如下文件：
    
    - 函数配置文件“function-config.json”
    - 函数入口文件“myCloudFunction.ts”
    - 依赖配置文件“package.json”
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155755.53458648776495118804064806163552:50001231000000:2800:2D7453701B01947818BD96E4C8481E6867758E010A3F98E4DF6A248BB7740BC3.png)
    

## 配置函数

函数创建完毕后，您可在配置文件“function-config.json”的“triggers”下配置触发器，通过触发器暴露的触发条件来实现函数调用。

说明

“functionType”表示函数类型，“0”表示云函数，“1”表示云对象。“functionType”的值为创建时自动生成，不可手动修改，否则将导致云函数部署失败。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155755.32981496705305715965328359294964:50001231000000:2800:BDE7A983FAAAC2FE10B5EF3311C642355A26F2D19A5F33E6256E2EA4698BB88A.png)

云函数当前仅支持HTTP触发器， “function-config.json”文件中已为您自动完成HTTP触发器配置。配置了HTTP触发器的函数被部署到云端后，您的应用即可通过Cloud Foundation Kit调用函数。关于如何使用HTTP触发器调用函数，请参见[调用函数](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-call-function)。

注意

如您需在函数部署完成后更新触发器，请先删除之前的触发器配置，再添加新的触发器配置，否则您的更新将不生效。

1. {
2.   "type": "http",
3.   "properties": {
4.     "enableUrlDecode": true,
5.     "authFlag": "true",
6.     "authAlgor": "HDA-SYSTEM",
7.     "authType": "apigw-client"
8.   }
9. }

- type：触发器类型，配置为“http”。
- properties：触发器属性，属性参数如下表所示。
    
    |参数|说明|
    |:--|:--|
    |enableUrlDecode|通过HTTP触发器触发函数时，对于contentType为“application/x-www-form-urlencoded”的触发请求，是否使用URLDecoder对请求body进行解码再转发到函数中。<br><br>- true：启用。<br>- false：不启用。|
    |authFlag|是否鉴权，默认为true。|
    |authAlgor|鉴权算法，默认为HDA-SYSTEM。|
    |authType|HTTP触发器的认证类型。<br><br>- apigw-client：端侧网关认证，适用于来自APP客户端侧（即本地应用或者项目）的函数调用。<br>- cloudgw-client：云侧网关认证，适用于来自APP服务器侧（即云函数）的函数调用。|
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-functionprocess "开发流程")
# 开发函数

更新时间: 2025-12-16 15:57

函数创建并配置完成后，您便可以开始编写函数业务代码了。

1. 打开函数入口文件，编写函数代码。关于开发函数代码的更详细信息，请参考[开发函数](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-develop-function-nodejs)。
    
    此处我们以函数“my-cloud-function”为例，构造一个用于返回时间戳的函数。
    
    1. /**
    2.  * Describe the basic method of Cloud Functions
    3.  */
    
    4. let myHandler = function(event, context, callback, logger){
    5.     // example of display environment variables
    6.     let env1 = context.env.env1;
    
    7.     // example of display logs
    8.     logger.info("Test info log");
    9.     logger.warn("Test warn log");
    10.     logger.debug("Test debug log");
    11.     logger.error("Test error log");
    
    12.     logger.info("--------Start-------");
    13.     try {
    14.         let startTime = new Date().getTime();
    15.         let endTime = startTime;
    16.         let interval = 0;
    17.         startTime = process.uptime() * 1000;
    
    18.         // print input parameters and environment variables
    19.         logger.info("request: " + JSON.stringify(event.request));
    20.         logger.info("env1: " + env1);
    
    21.         endTime = process.uptime() * 1000;
    22.         interval = endTime - startTime;
    23.         logger.info("intervalTime: " + interval);
    24.         logger.info("--------Finished-------");
    
    25.         let res = new context.HTTPResponse(context.env, {
    26.             "res-type": "context.env",
    27.             "faas-content-type": "json",
    28.         }, "application/json", "200");
    29.         res.body = {"intervalTime": interval};
    30.         callback(res);
    31.     } catch (error) {
    32.         logger.error("--------Error-------");
    33.         logger.error("error: " + error);
    34.         callback(error);
    35.     }
    36. };
    
    37. module.exports.myHandler = myHandler;
    
    注意
    
    云函数与云函数之间是相互独立的，部署至云侧时，只会部署所选云函数目录下的文件，不可在一个云函数中通过import '../anotherDirectory/xxx'的方式引入依赖。如果有多个云函数公共的配置，建议存储在云数据库中，通过云数据库Server API类查询出公共配置；也可以将多个云函数整合成一个云对象，将公共配置变成云对象的私有配置。
    

2. （可选）如函数存在依赖关系，可在“package.json”文件的“dependencies”下添加需要的依赖，然后点击右上角“Sync Now”。
    
    下文以添加“@hw-agconnect/cloud-server”依赖为例进行说明，请添加实际业务所需的依赖。
    
    说明
    
    右击“package.json”文件，选择“Run 'npm install'”菜单，也可以实现依赖包安装。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155756.46232991599764175789957889982253:50001231000000:2800:5A74EEF7B0C149CC68A136617594C84AE360AFD98E2009648B6FEAEA69A4E29A.png)
    
    所有安装的依赖包都会存储在当前函数的“node_modules”目录下。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155757.03250659709478578724757587264929:50001231000000:2800:6C6C67C5F700EA41714FA077847DBDE82E686394768246190203EFA0305E3119.png)
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-createfunc "创建并配置函数")
# 调试函数

更新时间: 2025-12-16 15:57

函数开发完成后，您可以对函数进行调试，以验证函数代码运行是否正常。

目前DevEco Studio函数调试支持本地调用和远程调用，请根据实际场景选择使用：

- [通过本地调用方式调试函数](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-debugfunc#section248615546567)：在DevEco Studio调试本地开发好的函数。支持单个调试和批量调试，并支持Run和Debug两种模式，调试功能丰富，常在函数开发过程或问题定位过程中使用。
- [通过远程调用方式调试函数](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-debugfunc#section123191549587)：先将函数部署至AGC云端，然后直接在DevEco Studio调用云端函数。此方式主要用于测试函数在云端的运行情况、或补充测试因各种因素限制未能在本地调用方式中发现的问题。

## 前提条件

- 请确保您已登录。
- 如果您的工程有代码逻辑涉及云函数调用云数据库，您需在调试前先[将整个云工程部署到AGC云端](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-deploy)，否则云端将没有相关数据及环境变量。

## 通过本地调用方式调试函数

您可在DevEco Studio调试本地开发好的函数，支持单个调试和批量调试，并支持Run和Debug两种模式。

- 单个调试和批量调试流程相同，区别仅在于：单个调试是一次只为一个函数启动本地调试，之后只能调用该函数；批量调试是一次为“cloudfunctions”目录下所有函数启动本地调试、然后逐个调用各个函数。
- Run模式和Debug模式的区别在于：Debug模式支持使用断点来追踪函数的运行情况，Run模式则不支持。

下文以Debug模式下调试单个函数“my-cloud-function”为例，介绍如何在DevEco Studio调试本地函数。

1. 右击“my-cloud-function”函数目录，选择“Debug 'my-cloud-function'”。
    
    说明
    
    - 直接从当前路径下Debug，使用的是默认的Debug配置，您也可[自定义Debug配置](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-debugfunc#section65830284215)。自定义Debug配置后再从此路径下Debug，将优先采用自定义Debug配置。
    - 如需批量调试多个函数，右击“cloudfunctions”目录，选择“Debug Cloud Functions”，即可启动该目录下所有函数。如“cloudfunctions”目录下同时存在云函数和云对象，将会启动所有的云函数和云对象。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155758.18859910487465051755593777060082:50001231000000:2800:CFAE65BE50EC1E01A628EE2D2E51862777329A644CC4DE2B830BF20A2F54E7BC.png)
    
2. 在下方通知栏“cloudfunctions”窗口，查看调试日志。如果出现“Cloud Functions loaded successfully”，表示函数成功加载到本地运行的HTTP Server中，并生成对应的Function URI。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155758.18171215111667214174016332569486:50001231000000:2800:5660FD44563C7DCFA2021F2580984F23EE78BA0D8C9122E6278EB0318CCF8A07.png)
    
3. 如需设置断点调试，在函数代码中选定要设置断点的有效代码行，在行号（如下图行15）后单击鼠标左键设置断点（如下图的红点）。
    
    设置断点后，调试能够在断点处中断，并高亮显示该行。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155758.35113355087590711123398266102040:50001231000000:2800:A07127CEAD45EE62FAB4CC7DD94D5E9EAEF1B9237FC0FD82CC2D09297757A71E.png)
    
4. 在菜单栏选择“View > Tool Windows > Cloud Functions Requestor”，使用事件模拟器（Cloud Functions Requestor）触发函数调用。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155758.30526958353288303449200454381278:50001231000000:2800:795EA93170DA4C3DFE6D089DA43A54F2377FC58FE561B3A87EA80375AC7F5075.png)
    
5. 在弹出的“Cloud Functions Requestor”面板，配置触发事件参数。
    
    - Cloud Function：选择需要触发的云函数，此处以函数“my-cloud-function”为例。
    - Environment：选择函数调用环境。此处选择“Local”，表示本地调用。
    - Event：输入事件参数，内容为JSON格式请求体数据。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155758.06845850879859970653940400674370:50001231000000:2800:203EB11FFC370F408FC7546431C493ADE1D35221574B0F69BA31BE57109C3DA6.png)
    
6. （可选）点击“Save”，可保存当前触发事件。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155758.35505199646554105657236321670345:50001231000000:2800:21A1F2486F17C0B645384FBBD1332E6B4F669790EC70DDC8D86E0A0C48B065BC.png)
    
    点击右上角![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155758.20872526377964682314257655244148:50001231000000:2800:FDF1C8A7C1F817024CF50FC7F9F3E2E951928F8FD662E95493D5A83B3F3B4BE9.png)可展开保存的触发事件，后续可直接点击“Load”加载事件。对于不需要保存的触发事件，也可以点击“Delete”删除。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155758.02264106826502923685147053176266:50001231000000:2800:B838BBF3C9401B66F8366E0B2B4C3EB8996DDC84419C5E6766F4337DAEA094CF.png)
    
7. 点击“Trigger”， 将会触发执行用户函数代码。执行结果将展示在“Result”框内，“cloudfunctions”窗口同时打印调试日志。
    
    说明
    
    “Result”框右侧的“Logs”面板仅用于在[通过远程调用方式调试函数](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-debugfunc#section123191549587)时查看日志。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155758.25135028497178826260569792178308:50001231000000:2800:6AAF7D350E55518AD404FAC3F605950C9520086FDF9BFDB00B795246DF0EAD42.png)
    
8. （可选）如[配置了环境变量](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-debugfunc#li15793566149)，可将变量信息传入到函数执行环境中，用于函数运行时读取。
    
    logger.info(context.env._name_);//name为环境变量名称
    
    如下图，函数“my-cloud-function”配置了环境变量“env1”，可成功访问环境变量“env1”的值“value1”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155758.11456014083101209722647979886123:50001231000000:2800:FB357FFA29098C33872000FAAE04CA0D94BF9E2CD6B2AE4047A82B9EDC26F126.png)
    
9. 点击菜单栏![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155758.48852185257675033617464824688361:50001231000000:2800:C20D77292C6F017BB52A2E750C7B3C37ABB63FB0266DAB6CC81CC75254BA4431.png)，可停止调试。
10. 根据调试结果修改函数代码后，点击![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155758.13809709244240457413422540916132:50001231000000:2800:5F6EB6F5880BD93A06334C28D3E5B79915987D35897BA452831499941266ECAA.png)重新以Debug模式启动调试，直至没有问题。
11. 参考步骤5~10，完成其他函数的调试。

## 通过远程调用方式调试函数

您还可以将函数部署至AGC云端，然后在DevEco Studio调用云端函数，以测试函数在云端的运行情况、或补充测试因各种因素限制未能在本地调试中发现的问题。

1. 参考[部署函数](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-deployfunc)将需要调试的函数部署至AGC云端。
2. （可选）如函数代码涉及访问环境变量，需在AGC Portal函数列表中点击函数名称，为函数配置环境变量的值，供函数在运行时读取和使用。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155758.03978403780959216271949888308364:50001231000000:2800:1A87EDB3B8930B1EAD642C9F949DF26DD9433B462D3AF697354C89E4C5578B01.png)
    
3. 在菜单栏选择“View > Tool Windows > Cloud Functions Requestor”，使用事件模拟器（Cloud Functions Requestor）触发函数调用。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155758.57686765710096827114251228859222:50001231000000:2800:E3804868E9AF84E13BDAF9E63A4BDBFA7E2A562E99E801E466C9AD2E19FDED36.png)
    
4. 在弹出的“Cloud Functions Requestor”面板，配置触发事件参数。
    
    - Cloud Function：选择需要触发的云函数，此处依然以函数“my-cloud-function”为例。
    - Environment：选择函数调用环境。此处选择“Remote”，表示远程调用。
    - Event：输入事件参数，内容为JSON格式请求体数据。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155758.98496175997904216293705559221525:50001231000000:2800:096D089699D9AC6F78A154895E3B58A7B2FAD50B91ACFE8F8103B5E273599E4A.png)
    
5. 点击“Trigger”， 将会触发执行用户函数代码，执行结果将展示在“Result”框内。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155759.98460324484925318796603545036665:50001231000000:2800:36A19F5718FF8C21C0886CC7CD031FCE2316FF625D33CC71D3CACA09AFBB6A7B.png)
    
6. 点击“Logs”页签，可查看打印的日志定位问题。修改函数代码、重新部署函数后再次执行远程调用，直至没有问题。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155759.31819844718793282437045101646605:50001231000000:2800:D7605B07C459468697C53C2EB12F3155D757EB469463104AE19BDB297FF39C16.png)
    
7. 参考步骤1~5，完成其他函数的调试。

## （可选）自定义Run/Debug配置

直接启动函数调试采用的是默认的Run/Debug配置。如有特殊需求，您也可使用自定义Run/Debug配置项来进行调试。

1. 在菜单栏选择“Run > Edit Configurations”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155759.69752590351415907590583376453193:50001231000000:2800:53EC34DB6E4CBEF9990030B8D8735CAED967D9C2A47653E8B3A5E9997D9D481A.png)
    
2. 在“Run/Debug Configurations”窗口，点击![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155759.07184851833659906776205448932856:50001231000000:2800:3B0A1EFB063B9D50C48D97508B8BCD7D14A7460689C7584F8BECC77E01052AAD.png)，选择“Cloud Functions”，新增一个Run/Debug配置。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155759.20998124584612640911883283009350:50001231000000:2800:0F15C62D5FB0A0960F7F6CA8C38125CE51699A396FADC84C886FE9437C8899EC.png)
    
3. 自定义Run/Debug配置，完成后点击“Run”或“Debug”即可立即按当前自定义配置启动本地调试。
    
    如当前暂不使用自定义配置，可点击“OK”保存配置。后续有需要时再选择自定义配置，分别点击![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155759.40487490870330828077655957495997:50001231000000:2800:B14C180E36965964650C68FB6543F8B8DC4772AECC50E32A0C3B44829DD4BEE4.png)或![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155759.43406365816786428586872848587684:50001231000000:2800:0BD6C580C1B3A506828FA5CA2C32B05FB1BA45578E59686F5B9FFCC61FD768D0.png)进行Run或Debug。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155759.69561785357906467076262447804360:50001231000000:2800:CDF374ED8E855773188A7F9C1384BE664D810158AE62675478A1C7DE7A4A2A56.png)
    
    - Name：Run/Debug配置的名称，如“functions-custom1”。
    - Server IP Address：HTTP服务端监听IP地址，默认为localhost，支持切换为您的局域网IP地址。
    - Server Port：HTTP服务端监听端口。默认为“18090”，自定义端口号建议大于1024。勾选“Auto increment”表示如当前端口被占用则端口号自动加“1”。
    - Environment variables：函数运行的环境变量，为key-value形式。
        
        点击“Edit environment variables”按钮，在“Environment Variables”弹窗中点击“+”添加一个环境变量，然后点击“OK”。添加成功后，您便可以将变量配置信息传入到函数执行环境中，用于函数运行时读取。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155759.87656049242546193895687724612866:50001231000000:2800:7A60AB62556FFABDA7C88CCEB2FF0B92CCA2BC3B7658AE5A9D243E2893C21DCD.png)
        
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-funccoding "开发函数")
# 部署函数

更新时间: 2025-12-16 15:58

完成函数代码开发后，您可将函数部署到AGC云端，支持单个部署和批量部署。

单个部署仅部署选中的函数，批量部署则会将整个“cloudfunctions”目录下的所有函数同时部署到AGC云端。

下文以部署单个函数“my-cloud-function”为例，介绍如何部署函数。

1. 右击“my-cloud-function”函数目录，选择“Deploy 'my-cloud-function'”。
    
    说明
    
    如需批量部署多个函数，右击“cloudfunctions”目录，选择“Deploy Cloud Functions”即可部署该目录下所有函数。如“cloudfunctions”目录下同时存在云函数和云对象，云函数和云对象将会被一起部署到AGC云端。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155801.75701673390003246951231620180531:50001231000000:2800:169D1CF768043D74EFDEA695DD3C8C4936DA61D1A410FC73EC1B1F32DF7DFB2C.png)
    
2. 您可在底部状态栏右侧查看函数打包与部署进度。
    
    请您耐心等待，直至出现“Deploy successfully”消息，表示当前函数已成功部署。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155801.41937645567728229690548432785788:50001231000000:2800:7E589A812D22BBEC98E1D12335CDEC517B9C254B805297F00C29EC5B0FD62A23.png)
    
3. 在菜单栏选择“Tools > CloudDev”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155801.95499194954059723240450160550071:50001231000000:2800:B1185AA9734FE91AD57DC593E3A2BAD46B9D57CB4A66368B3CE924AA2A266694.png)
    
4. 在打开的CloudDev面板中，点击“Serverless > Cloud Functions”下的“Go to console”，进入当前项目的云函数服务页面。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155801.07813284557895716021037811089140:50001231000000:2800:FA8ECA460C05F37743BF5DF7BBF1FDD906CE27F8DA570D7DB3E64EC7F1A1AF84.png)
    
5. 查看到“my-cloud-function”函数已成功部署至AGC云端，函数名称与本地工程的函数目录名相同。
    
    部署成功后，您便可以从端侧调用云函数了，具体请参见[在端侧调用云函数](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-invokecloudfunc)。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155801.36860649613711288461911963176157:50001231000000:2800:FA494B5712BE0D0592B8F72C437E02CFC813FB6DA8416B9B9489FD241AC91B09.png)
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-debugfunc "调试函数")
# 开发流程

更新时间: 2025-12-16 15:57

除去传统的云函数，您还可在端云一体化云侧工程下开发云对象。云对象是一种特殊的云函数，本质是对云函数的一种封装，客户端可通过导入一个云对象来直接使用这个对象的方法，为您提供在端侧直接调用云侧代码的开发体验。相对普通云函数方式，云对象代码更精简、逻辑更清晰，大多数场景下推荐使用云对象代替传统云函数。开发流程大致如下：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155755.31217567691347977841961189522643:50001231000000:2800:97C79EED052115B679BD158FBAF94697042B95AC812CB8EBFA7825262E53A3DA.png "点击放大")

1. [创建云对象](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-createcloudobj)：您可直接在DevEco Studio创建云对象。
2. [开发云对象](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-cloudobj-coding)：云对象创建完成后，您便可以开始编写云对象业务代码了。
3. [调试云对象](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-debugcloudobj)：您可以对云对象进行调试，以测试云对象代码运行是否正确。
4. [部署云对象](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-deploycloudobj)：完成云对象代码开发与调试后，您可将云对象部署到AGC云端，支持单个部署和批量部署。

说明

一般建议先将云对象调试无误后再部署至云端，但某些业务场景下需要先部署云对象才能进行调试。请根据实际业务需要操作。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-cloudobj "开发云对象")
# 创建云对象

更新时间: 2025-12-16 15:57

首先您需要在云侧工程下创建云对象。

1. 右击“cloudfunctions”目录，选择“New > Cloud Function”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155755.73244909589914712235640631562164:50001231000000:2800:DF25BA6B58050C187DF46A64EF9A5EE4F007A97BEC534A11439D44A35A9D8B45.png)
    
2. 在“Select the Cloud Function Type”栏选择“Cloud Object”，输入云对象名称（如“my-cloud-object”），点击“OK”。
    
    与云函数名一样，云对象名称长度2-63个字符，仅支持小写英文字母、数字、中划线（-），首字符必须为小写字母，结尾不能为中划线（-）。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155755.47657019742259790375970695837167:50001231000000:2800:3C29CB0C7D75B6F06168A72AA4A0141762D5E7B4C5CB7406EB03994940BE8000.png)
    
    “cloudfunctions”目录下生成新建的云对象目录，目录下主要包含如下文件：
    
    - 云对象配置文件“function-config.json”：包含handler、触发器等信息。
        
        - handler: 云对象的入口模块及云对象导出的类，通过“.”连接。
        - functionType：表示函数类型，“0”表示云函数，“1”表示云对象。
        - triggers：定义了云对象使用的触发器类型，当前云对象仅支持HTTP触发器。
        
        说明
        
        云对象的配置文件“function-config.json”不建议手动修改，否则将导致云对象部署失败或其它错误。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155755.84341079117794600787893562554781:50001231000000:2800:05402A400E2D4905F73A0CE9C23DD1088A69960B208447132DBE26CD75C425DB.png)
        
    - 云对象入口文件“_xxx_.ts”（如“myCloudObject.ts”）：在此文件中编写云对象代码。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155755.91995828495014410642149386941073:50001231000000:2800:F61F688F256E21C957F993CE6C649CB24CE22003B091E06D22AC5000F8525642.png)
        
    - 云对象依赖配置文件“package.json”：在此文件中添加依赖。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155755.78731143157557333539622354563582:50001231000000:2800:8FB70353B5CFF88F3CA155F30C83AD610B05433524CFD100929F5857D67323F9.png)
        
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-cloudobjprocess "开发流程")
# 开发云对象

更新时间: 2025-12-16 15:57

云对象创建完成后，您便可以直接在云对象中编写需要实现的方法。例如，通过云对象实现add与subtract两个方法。

1. 打开云对象入口文件（此处以“myCloudObject.ts”为例），添加add与subtract方法。
    
    1. export class MyCloudObject {
    2.     add(num1: number, num2: number) {
    3.         return { result: num1 + num2 };
    4.     }
    5.     subtract(num1: number, num2: number) {
    6.         return { result: num1 - num2 };
    7.     }
    8. }
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155757.19975402190557376334231620677371:50001231000000:2800:C997413B3E1C732EDBD20407EC9A85F7AE9BD7029579744331433776044B4A74.png)
    
    注意
    
    - 云对象是无状态性。云对象部署至云侧后，每一次调用都可能是不同的后台节点，因此在云对象上定义类成员变量是无意义的。从一个Method中对一个类成员属性赋值，然后期望从另一个Method去获取类成员属性，这样的做法是错误的。
    - 云对象无需编写构造函数。云侧在收到对云对象的某一个函数的请求时，会调用云对象的默认的无参构造函数。
    - 云对象方法的输入是从JSON反序列化而来，只能是string、number或者Object，不支持Date、Uint8Array等类型。如果在编写云对象代码的过程中需要传递Date或Uint8Array，建议通过定义成number或者数组，在Method内通过显式地调用Date或Uint8Array的构造函数来达到目的。
    - 云对象的方法的输出当前不支持单个number返回。
    - 云对象的方法的输入、输出可以使用自定义对象，不能使用第三方依赖定义的对象或类型。注意，并不是云对象不能有第三方依赖，而是云对象的输入和输出不能有第三方依赖，否则在"Generator Invoke Interface"阶段，将会因为找不到依赖而失败，根本原因是，端侧代码运行在HarmonyOS支持方舟运行时，而云侧运行在Node.js中，二者的依赖管理不同。
    

2. （可选）如云对象存在依赖关系，可在“package.json”文件的“dependencies”下添加需要的依赖，然后点击右上角“Sync Now”。
    
    下文以添加“@hw-agconnect/cloud-server”依赖为例进行说明，请添加实际业务所需的依赖。
    
    说明
    
    右击“package.json”文件，选择“Run 'npm install'”菜单，也可以实现依赖包安装。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155757.02260563866938459143653670436085:50001231000000:2800:8C31D065B318FDE37824B21F91CA4BC07D7D5267FDD69E57384888028BD66A12.png)
    
    所有安装的依赖包都会存储在当前云对象的“node_modules”目录下。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155757.20541237972141996355923893893855:50001231000000:2800:CDDBBFBFB8E47C1A38294D847C5A684E63B8ABEBBD39066EBB50F9ED672503FB.png)
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-createcloudobj "创建云对象")
# 调试云对象

更新时间: 2025-12-16 15:58

云对象开发完成后，您可以对其进行调试，以验证云对象代码运行是否正常。

目前DevEco Studio云对象调试支持本地调用和远程调用，请根据实际场景选择使用：

- [通过本地调用方式调试云对象](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-debugcloudobj#section248615546567)：在DevEco Studio调试本地开发好的云对象。支持单个调试和批量调试，并支持Run和Debug两种模式，调试功能丰富，常在云对象开发过程或问题定位过程中使用。
- [通过远程调用方式调试云对象](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-debugcloudobj#section123191549587)：先将云对象部署至AGC云端，然后直接在DevEco Studio调用云端云对象。此方式主要用于测试云对象在云端的运行情况、或补充测试因各种因素限制未能在本地调用方式中发现的问题。

## 前提条件

- 请确保您已登录。
- 如果您的工程有代码逻辑涉及云对象调用云数据库，您需在调试前先[将整个云工程部署到AGC云端](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-deploy)，否则云端将没有相关数据及环境变量。

## 通过本地调用方式调试云对象

您可在DevEco Studio调试本地开发好的云对象，支持单个调试和批量调试，并支持Run和Debug两种模式。

- 单个调试和批量调试流程相同，区别仅在于：单个调试是一次只为一个云对象启动本地调试，之后只能调用该云对象；批量调试是一次为“cloudfunctions”目录下所有云对象启动本地调试、然后逐个调用各个云对象。
- Run模式和Debug模式的区别在于：Debug模式支持使用断点来追踪云对象的运行情况，Run模式则不支持。

下文以Debug模式下调试单个云对象“my-cloud-object”为例，介绍如何在DevEco Studio调试本地云对象。

1. 右击“my-cloud-object”云对象目录，选择“Debug 'my-cloud-object'”。
    
    说明
    
    - 如需批量调试多个云对象，右击“cloudfunctions”目录，选择“Debug Cloud Functions”，即可启动该目录下所有云对象。如“cloudfunctions”目录下同时存在云函数和云对象，将会启动所有的云函数和云对象。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155759.71855554268959851448171564273151:50001231000000:2800:8275583B5EBE4BC0349423930F1C93D523E23416423ED43ECA0ABA4C072EE25C.png)
    
2. 在下方通知栏“cloudfunctions”窗口，查看调试日志。如果出现“Cloud Functions loaded successfully”，表示云对象已成功加载到本地运行的HTTP Server中，并生成对应的Function URI。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155759.27467719522909506722190897525829:50001231000000:2800:22F66ED0A34683033AF4B6086DD9154AAB6731C242E1FB53FB14C43253E705CE.png)
    
3. 如需设置断点调试，在函数代码中选定要设置断点的有效代码行，在行号（如下图行3）后单击鼠标左键设置断点（如下图的红点）。
    
    设置断点后，调试能够在断点处中断，并高亮显示该行。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155759.63980104491319073858492162620301:50001231000000:2800:57CAF9945505C1D6CE55ED8093E605EDC00134CA8100209222D1A529E602FA58.png)
    
4. 在菜单栏选择“View > Tool Windows > Cloud Functions Requestor”，使用事件模拟器（Cloud Functions Requestor）触发云对象调用。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155759.67928755908212196071351126173073:50001231000000:2800:026DF6C3703B514484C69AABD0EF5541A1B65F47A8441D4644F49A4D117CF3E7.png)
    
5. 在弹出的“Cloud Functions Requestor”面板，配置触发事件参数。
    
    - Cloud Function：选择需要触发的云对象，此处以云对象“my-cloud-object”为例。
    - Environment：选择云对象调用环境。此处选择“Local”，表示本地调用。
    - Method：必填项，输入云对象的方法名称，如“add”。
    - Event：方法参数列表，JSON array格式，依次代表Method的入参。如add方法接收两个number类型的形参，num1与num2，那么填入“[1, 2]”表示构造num1=1，num2=2的请求。
        
        注意
        
        如果Method的入参中的某一个是数组[]类型，那么Event中将至少包含两层方括号，如'[[1, 2], 3]'，外层的方括号表示参数列表。
        
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155759.79906847307357781526870084374125:50001231000000:2800:E227F2D4C2512402CEF584E7DF4499E768B8B4AA8F7D3A604EF677A6A19AD708.png)
    
6. （可选）点击“Save”，可保存当前触发事件。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155759.31846617724977360983490319507135:50001231000000:2800:D8CAAF7B9103EA9538A4B5A19A929843606208C2C69E630419E4E31BA53443AE.png)
    
    点击右上角![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155759.32930618899926802247903672492763:50001231000000:2800:E3F47FBA289F07E3C15B003177BDD1FAAF1C3EF6109D1486927D94E89AA2197B.png)可展开保存的触发事件，后续可直接点击“Load”加载事件。对于不需要保存的触发事件，也可以点击“Delete”删除。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155759.57778562446315417537891110746039:50001231000000:2800:07DFE3D41CDC72E6843036CDDB675E73D0EB8481F5F9EC5532B4A4D411279D22.png)
    
7. 点击“Trigger”， 将会触发执行云对象的方法，执行结果将展示在“Result”框内。
    
    说明
    
    “Result”框右侧的“Logs”面板仅用于在[通过远程调用方式调试云对象](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-debugcloudobj#section123191549587)时查看日志。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155800.72992920114444742560704649828351:50001231000000:2800:72A10F67E7B72D426E8203E9DCECAADF82D4F569200DF8235E5C9F4FD0F9FE74.png)
    
8. 点击菜单栏![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155800.48217222551865325075288862633065:50001231000000:2800:0F46CF6A57C70E4D608FB9E70C48541EF507FED7BBE16CC308F70B71411DAAD9.png)，可停止调试。
9. 根据调试结果修改云对象代码后，点击![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155800.35312711392450810598386132239004:50001231000000:2800:8E4183C6332F944BF9BAAD3A5487BF1803B915621B9F9DBF6E86A1F126F911E3.png)重新以Debug模式启动调试，直至没有问题。
10. 参考步骤5~9，完成云对象其他方法或其他云对象的调试。

## 通过远程调用方式调试云对象

您还可以将云对象部署至AGC云端，然后在DevEco Studio调用云端云对象，以测试云对象在云端的运行情况、或补充测试因各种因素限制未能在本地调试中发现的问题。

1. 参考[部署云对象](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-deploycloudobj)将需要调试的云对象部署至AGC云端。
2. 在菜单栏选择“View > Tool Windows > Cloud Functions Requestor”，使用事件模拟器（Cloud Functions Requestor）触发云对象调用。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155800.03211094285602086849519606140693:50001231000000:2800:E8CB348DA78159C1C100530002568C4009753037D4B7EDDDEAF3D4D2C9F8A3E4.png)
    
3. 在弹出的“Cloud Functions Requestor”面板，配置触发事件参数。
    
    - Cloud Function：选择需要触发的云对象，此处依然以“my-cloud-object”为例。
    - Environment：选择云对象调用环境。此处选择“Remote”，表示远程调用。
    - Method：输入云对象的方法名称，如“add”。
    - Event：方法参数列表，JSON array格式，按顺序代表Method的入参，如add方法接收两个number类型的形参，num1与num2，那么填入“[1, 2]”表示构造num1=1，num2=2的请求，如“[1, 2]”。
        
        注意
        
        如果Method的入参中的某一个是数组[]类型，那么Event中将至少包含两层方括号，如'[[1, 2], 3]'，外层的方括号表示参数列表。
        
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155800.44812571132728788698274126678876:50001231000000:2800:016E30579702394FF76D5DF8B26C782F7196EC6DA9908641539EDE6885D04AA9.png)
    
4. 点击“Trigger”， 将会触发执行云对象方法，执行结果将展示在“Result”框内。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155800.34759526149913858009314278407214:50001231000000:2800:A96AB65FBE051D2DD24E0FBD6AC9A9F900F246700F17556BCACADA2C3AD41A61.png)
    
5. 点击“Logs”页签，还可查看打印的日志定位问题。修改云对象代码、重新部署云对象后再次执行远程调用，直至没有问题。
6. 参考步骤1~5，完成云对象其他方法或其他云对象的调试。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-cloudobj-coding "开发云对象")
# 部署云对象

更新时间: 2025-12-16 15:58

完成云对象代码开发后，您可将云对象部署到AGC云端，支持单个部署和批量部署。

单个部署仅部署选中的云对象，批量部署则会将整个“cloudfunctions”目录下的所有云对象同时部署到AGC云端。

下文以部署单个云对象“my-cloud-object”为例，介绍如何部署云对象。

1. 右击“my-cloud-object”云对象目录，选择“Deploy 'my-cloud-object'”。
    
    说明
    
    如需批量部署多个云对象，右击“cloudfunctions”目录，选择“Deploy Cloud Functions”即可部署该目录下所有云对象。如“cloudfunctions”目录下同时存在云函数和云对象，云函数和云对象将会被一起部署到AGC云端。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155801.58630058078140854230497294793121:50001231000000:2800:B19F55FDAD7B016A82DE8F66C249290FB61D76403417838CE2401045FF8A2FFA.png)
    
2. 您可在底部状态栏右侧查看云对象打包与部署进度。
    
    请您耐心等待，直至出现“Deploy successfully”消息，表示当前云对象已成功部署。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155801.77854698377155361025141435210987:50001231000000:2800:3101601FF41AB9792E9C64C955D578BD6BB6E8FBDF541923793942BEA8C80889.png)
    
3. 在菜单栏选择“Tools > CloudDev”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155801.43413563402043485367524673291737:50001231000000:2800:A684E72874EA87DB3C2CA1D8CA4CB3CE0D5081B7EC2C55D709795CAA9FB0F0A1.png)
    
4. 在打开的CloudDev面板中，点击“Serverless > Cloud Functions”下的“Go to console”，进入当前项目的云函数服务页面。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155801.83407106977226160311097473428038:50001231000000:2800:D5B73DF0F6C5CA40B3FFE6D2A68BCECD490A94247D8BCD6AB8903022A5255E09.png)
    
5. 查看到“my-cloud-object”云对象已成功部署至AGC云端，云对象名称与本地工程的云对象目录名相同。
    
    部署成功后，您便可以从端侧调用云对象了，具体请参见[在端侧调用云对象](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-invokecloudobj)。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155801.63254909716008752766315286230654:50001231000000:2800:85663E3F2BA57F9BFA51945E69445B1F8228C02CD0D569A12B152B298C04C82F.png)
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-debugcloudobj "调试云对象")
# 开发流程

更新时间: 2025-12-16 15:57

|   |   |
|---|---|
|云数据库是一款端云协同的数据库产品，提供端云数据的协同管理、统一的数据模型和丰富的数据管理API接口等能力。云数据库采用基于对象模型的数据存储结构。<br><br>- 数据以对象（Object）的形式存储在不同的存储区中，每一个对象，都是一条完整的数据记录。<br>- 对象类型（ObjectType）用于定义存储对象的集合，不同的对象类型对应的不同数据结构。<br>- 存储区（Zone）是一个独立的数据存储区域，每个存储区拥有完全相同的对象类型定义。|![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155755.17181602433494012616980599325938:50001231000000:2800:61EC9A31E31A83E0A5F74066FE1B11C9D7A23CD4866DCC74BDDD6049E894CBA9.png "点击放大")|

您可以使用DevEco Studio在端云一体化云侧工程下开发云数据库，总体流程如下。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155755.32132435891543507534394708201283:50001231000000:2800:1A4F2EE0E3CF050264FE7F8AEEE708BBE8FB42DA5475A837699724936088C2B8.png "点击放大")

1. [创建对象类型](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-objecttype)：创建一个用于存储数据条目的对象类型。
2. [添加数据条目](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-dataentry)：在刚刚创建的对象类型内添加一条条数据，并配置数据所在的存储区。
3. [部署云数据库](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-deploydatabase)：数据成功添加后，您可以直接将该数据部署至AGC云端。您也可以等所有对象类型和数据条目开发完成后，再统一批量部署到AGC云端。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-clouddb "开发云数据库")
# 创建对象类型

更新时间: 2025-12-16 15:57

对象类型（ObjectType）用于定义存储对象的集合，不同的对象类型对应的不同数据结构。每创建一个对象类型，云数据库会在每个存储区实例化一个与之结构相对应的对象类型，用于存储对应的数据。

创建对象类型的操作如下：

1. 右击“clouddb/objecttype”目录，选择“New > Cloud DB Object Type”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155756.71826068690328065366278252080743:50001231000000:2800:6C8671159E6F3AE3345D3443C8793E69E7A8FE2302E370625031C3FDC1B267A9.png)
    

2. 输入对象类型名称（下文以“objecttype1”为例）后，点击“OK”。
    
    说明
    
    对象类型名称必须符合如下规范：
    
    - 只能包含字母（A-Z或a-z）、数字（0-9）和下划线（_），并且至少包含字母类型。
    - 必须以字母开头，以字母或者数字结尾，不允许以“sqlite_”开头，不允许以下划线（_）结尾。
    - 不允许使用如下系统保留名称： naturalbase_metadata、objecttypeinfohelper、t_data_upgrade_info、t_index_schema、t_nstore_config、t_schema_negotiate_info、t_metadata_schema、t_nstore_permission、t_system_config。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155756.01185577284063894783768070589522:50001231000000:2800:1A310D03E92CF4CBBB246A249672D2804D1A90F6634FBBCFB406B46C3DCB6ED9.png)
    
    “clouddb/objecttype”目录下生成并打开新建的对象类型JSON文件“objecttype1.json”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155756.15273860627804972082422463630185:50001231000000:2800:3496D2FF513487FBDECC641BDD6E5BBC568952234DE2406EFA5C14BA0F45BE49.png)
    
3. 在“fields”中为该对象类型配置字段信息。
    
    |参数|必选(M)/可选(O)|说明|
    |:--|:--|:--|
    |fieldName|M|字段名称。<br><br>输入要求具体如下：<br><br>- 字段的名称长度必须大于或等于1个字符，小于或等于30个字符，只能包含以下3种类型，并且至少包含“字母”类型：<br>    - 字母（A-Z或a-z）<br>    - 数字（0-9）<br>    - 特殊字符：_<br>- 字段名称必须以字母开头，以字母或者数字结尾。<br>- 字段名称中不区分字母的大小写。<br>- 修改对象类型时，支持删除字段。<br>- 字段名称不允许使用系统保留字段名称： naturalbase_version、naturalbase_deleted、naturalbase_operationtype、naturalbase_creator、naturalbase_accesstime、naturalbase_operationtime、naturalbase_syncstatus、naturalbase_changedfieldsbitmap、naturalbase_lastmodifier、cmin、cmax、xmin、xmax、ctid、oid、tableoid、xc_node_id、tablebucketid、rowid。<br><br>说明<br><br>当前Cloud Foundation Kit暂不支持自增类型字段IntAutoIncrement或LongAutoIncrement。|
    |fieldType|M|字段的数据类型。<br><br>当前支持的数据类型：String、Boolean、Byte、Short、Integer、Long、Float、Double、ByteArray、Text、Date。|
    |belongPrimaryKey|O|设置该字段是否为对象类型的主键，默认值为false。<br><br>- 至少设置一个字段为主键。<br>- 支持设置复合主键，由多个字段组合成为主键，一个复合主键包含的字段小于等于5个，复合主键字段顺序与字段的顺序一致。<br>- 数据类型为ByteArray、Text、Date、Double、Float和Boolean的字段不支持设置为主键。<br>- 主键的值不允许更改。|
    |notNull|O|设置字段值是否为非空，默认值为false。<br><br>- 数据类型为ByteArray和Date的字段不支持设置为非空。<br>- 主键默认非空，且不允许更改。<br>- 设置为非空的字段不支持加密和敏感。|
    |isNeedEncrypt|O|设置字段是否需要加密，开启全程加密数据管理功能，默认值为false。<br><br>选择加密后，该字段对应的数据会加密存储在存储区中。<br><br>- 主键字段不支持加密。<br>- 加密的字段不支持设置为非空。<br>- 加密的字段不支持设置为敏感字段。<br>- 一个对象类型中包含的加密字段和敏感字段的总数需小于或等于5个。<br>- 字段设置为加密后，不支持导出该字段的数据值。<br>- 数据类型为ByteArray、Text的字段不支持加密。<br>- 对象类型创建成功后，不支持修改加密属性。|
    |isSensitive|O|设置字段是否为敏感字段，默认值为false。<br><br>选择敏感后，该字段对应的数据会加密存储在存储区中。<br><br>- 敏感字段不支持设置为主键。<br>- 敏感字段不支持设置为非空。<br>- 敏感字段不支持设置为加密。<br>- 敏感字段不支持设置为默认值。<br>- 对象类型创建成功后，不支持修改敏感属性。<br>- 仅支持数据类型为Byte、Short、Integer、Long、Float、Double、String和Date的字段设置为敏感字段。<br>- 敏感字段不支持设置为索引。<br>- 一个对象类型中包含的加密字段和敏感字段的总数需小于或等于5个。|
    |defaultValue|O|字段为非空时，必须设置默认值。<br><br>- 主键不支持设置默认值。<br>- 加密字段和敏感字段不支持设置默认值。<br>- 数据类型为ByteArray、Date不支持为其设置默认值。<br>- 数据类型为Text的字段设置默认值时，默认值的长度小于或等于200个字符。|
    
    例如，我们可为“objecttype1”对象类型配置如下字段。
    
    |fieldName|fieldType|belongPrimaryKey|notNull|isNeedEncrypt|defaultValue|
    |:--|:--|:--|:--|:--|:--|
    |author|String|true|true|-|-|
    |shadowFlag|Boolean|-|true|-|true|
    |bookName|String|-|-|-|-|
    |id|Integer|-|-|-|-|
    |price|Double|-|-|-|-|
    |publishTime|Date|-|-|-|-|
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155756.66976924199962607540953887004242:50001231000000:2800:88CE497FE4102D570A65CB1DA3A89B7084970681001EC809DC00A7AEE38E3E18.png)
    
4. 在“indexes”中为该对象类型配置索引、索引包含的字段、以及索引包含的字段的排序方式。
    
    |参数|必选(M)/可选(O)|说明|
    |:--|:--|:--|
    |indexName|M|索引名称。<br><br>输入要求具体如下：<br><br>- 索引的名称长度必须大于或等于1个字符，小于或等于30个字符，只能包含以下3种类型，并且至少包含“字母”类型：<br>    - 字母（A-Z或a-z）<br>    - 数字（0-9）<br>    - 特殊字符：_<br>- 索引名称必须以字母开头。<br>- 索引名称中不区分字母的大小写。<br>- 修改对象类型时，仅支持新增或者删除索引。当删除索引后，本次提交前不允许新增同名索引。<br>- 每个对象类型可以设置小于或等于16个索引。<br>- 数据类型为ByteArray和Text的字段不支持设置为索引。|
    |indexList > fieldName|M|索引包含的字段。<br><br>支持设置组合索引，由多个字段组合成为索引，一个组合索引包含的字段不超过5个。|
    |indexList > sortType|M|索引包含的字段的排序方式，支持升序或降序。|
    
    例如，我们可为“objecttype1”对象类型配置如下两个索引。
    
    |indexName|fieldName|sortType|
    |:--|:--|:--|
    |id_Index|id|ASC|
    |price_Index|price|DESC|
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155756.26528015447767909113378981140376:50001231000000:2800:3B409A484FF9640C7CEC7D484B405C81263ECFF1F59588100AACF2A59540A4E9.png)
    
5. 在“permissions”中设置各角色是否具有该对象类型的Read、Upsert（包含新增和修改）和Delete权限。
    
    |参数|必选(M)/可选(O)|说明|
    |:--|:--|:--|
    |role|M|用户角色，包括：<br><br>- World：代表所有用户，包含认证和非认证用户。该角色默认拥有Read权限，可自定义配置Upsert和Delete权限。但是，不建议将Upsert和Delete权限配置给所有人角色。当对象类型中设置了加密字段之后，表示开启全程加密功能，此时所有人角色将不会拥有Read、Upsert和Delete权限，且不允许修改。<br>- Authenticated：经过AGC登录认证的用户。该角色默认拥有Read权限，可自定义配置Upsert和Delete权限。当对象类型中设置了加密字段之后，表示开启全程加密功能，此时认证用户角色将不会拥有Read、Upsert和Delete权限，且不允许修改。<br>- Creator：经过认证的数据创建用户。该角色默认拥有所有权限，且可自定义配置所有权限。每条数据都有其对应的数据创建人（即应用用户），每个数据创建者仅可以Upsert或者Delete自己创建的数据，不能Upsert或者Delete他人创建的数据。数据创建者的信息保存在数据记录的系统表中。<br>- Administrator：应用开发者，主要是指通过AGC控制台或FaaS（Function as a Service，函数即服务）侧访问云数据库的角色。该角色默认拥有所有权限，且可自定义配置所有权限。Administrator可以管理并配置其他角色的权限。|
    |rights|M|授予角色的权限，包括Read、Upsert（包含新增和修改）和Delete权限。|
    
    说明
    
    各角色只能完成对应权限的操作，超出权限范围的操作云侧将返回“permission denied”错误。由于端云一体化工程的初始化代码未[配置AccessToken](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/cloudfoundation-cloudcommon#section9723191765120)，故“CloudProgram/clouddb/objecttype/Post.json”中给World角色添加了Upsert和Delete权限。
    
    例如，我们可按下表为各个角色配置“objecttype1”对象类型的权限。
    
    |角色|Read|Upsert|Delete|
    |:--|:--|:--|:--|
    |World|√|–|–|
    |Authenticated|√|√|–|
    |Creator|√|√|√|
    |Administrator|√|√|√|
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155756.95380571954949769397635709637734:50001231000000:2800:D0145671D2D3ED1FCA4CA3EEB83EC22FF1047F9155C539F5C5E440D85E9A9B7E.png)
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-dbprocess "开发流程")
# 添加数据条目

更新时间: 2025-12-16 15:57

创建完对象类型后，您可在对象类型内添加数据条目（DataEntry），并配置数据所在的存储区。

支持手动创建和自动生成数据条目文件。

## 手动创建数据条目文件

1. 右击“clouddb/dataentry”目录，选择“New > Cloud DB Data Entry”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155757.71211765838168872454202164881854:50001231000000:2800:02B8E81015F3BD41F3B8A649147DA3E2C8E61C857D9157752468133164F60FE5.png)
    

2. 在“Associated Cloud DB Object Type”栏选择需添加数据条目的对象类型，在“Enter Cloud DB Data Entry Name”栏定义数据条目文件名，完成后点击“OK”。
    
    例如，选择刚刚创建的对象类型“objecttype1”，数据条目文件取默认名“d_objecttype1”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155757.88613863309132977925218649251382:50001231000000:2800:2D16AC1DFC092B8D98864E246B7237C24A1ED52A724D8901BD708F470E8ABACB.png)
    
    如下图，“clouddb/dataentry”目录下生成并打开新建的数据条目JSON文件“d_objecttype1”，该文件中已为您预置好所属对象类型名称（“objecttype1”）与对象类型的字段名（“id”、“bookName”、“author”、“price”、“publishTime”、“shadowFlag”）。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155757.14080375154413081890601477505456:50001231000000:2800:12D3E9DA3BA401AB8592CECA2EB82A2B7CE037FA3FAC720B56CA60BD20AF0E54.png)
    
3. 配置存储区和字段的值（即数据）。
    
    - “cloudDBZoneName”：配置存储区名称。上图示例中的“default”表示添加数据条目至default存储区。支持修改，如下图“cloudDBZoneName1”。另外，在使用API访问云数据库编码时需要引用该字段。
    - “objects”：配置当前对象类型中所有字段的值，即写入数据。一个对象（object）即为一条数据，您可以通过新建一个对象（object）来为字段赋新值，也可以修改某个对象（object）下字段的值（主键或加密字段的值不支持修改）。如下图，写入了两条数据。
        
        |字段|数据条目1|数据条目2|
        |:--|:--|:--|
        |author|Nancy|Peter|
        |shadowFlag|true|false|
        |bookName|My Favorite Book|Your First English Book|
        |id|10|20|
        |price|10.5|20.5|
        |publishTime|19961007|19961007|
        
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155757.09589891954401941227135121782288:50001231000000:2800:EC0EF7E30AE65252DD1D75965DC669E7789F1E4457523ECDEF135336729F1C13.png)
    

## 自动生成数据条目文件

1. 右击对象类型JSON文件，选择“Generate Data Entry”。
    
    依旧以对象类型“objecttype1”为例，其包含了“id”、“bookName”、“author”、“price”、“publishTime”、“shadowFlag”六个字段。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155757.37805171993341042197964512170084:50001231000000:2800:183EC9EA18F527C7990B5710A263DAE5E8EE8EDE1DF8E99E1B94904ED9EE212C.png)
    

2. 在弹出的“New Cloud DB Data Entry”框内，为即将生成的数据条目文件定义名称。此处取默认值“d_objecttype1”为例。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155757.31017682485871345529431328683882:50001231000000:2800:FC17303A5127CFE7B0D19730878F3FD58666702ED0BFA5BDDF25A56B9CB0415D.png)
    
    如下图，“clouddb/dataentry”目录下自动为对象类型“objecttype1”生成数据条目文件“d_objecttype1”，该文件中已为您预置好所属对象类型名称（“objecttype1”）与对象类型的字段名（“id”、“bookName”、“author”、“price”、“publishTime”、“shadowFlag”）。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155757.42690517352263846308939151902609:50001231000000:2800:067045C3540A49417F9CE11A809F8780E6FC50E4D4A3160A0D278844CB7AE8DC.png)
    
3. 配置存储区和字段的值（即数据）。
    
    - “cloudDBZoneName”：配置存储区名称。上图示例中的“default”表示添加数据条目至default存储区。支持修改，如下图“cloudDBZoneName1”。另外，在使用API访问云数据库编码时需要引用该字段。
    - “objects”：配置当前对象类型中所有字段的值，即写入数据。一个对象（object）即为一条数据，您可以通过新建一个对象（object）来为字段赋新值，也可以修改某个对象（object）下字段的值（主键或加密字段的值不支持修改）。如下图，写入了两条数据。
        
        |字段|数据条目1|数据条目2|
        |:--|:--|:--|
        |author|Nancy|Peter|
        |shadowFlag|true|false|
        |bookName|My Favorite Book|Your First English Book|
        |id|10|20|
        |price|10.5|20.5|
        |publishTime|19961007|19961007|
        
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155757.84374636493900212303330368511807:50001231000000:2800:A6D157E9118C3EE443B78908C7A6124F26C16B1EADD93BE2812BED4FC040B7DE.png)
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-objecttype "创建对象类型")
# 部署云数据库

更新时间: 2025-12-16 15:58

完成数据条目创建后，您可以直接部署该数据条目。您也可以等所有对象类型和数据条目开发完成后，再统一批量部署到AGC云端。

说明

- 部署到AGC云端的存储区数量不得超过4个，否则会导致部署失败，提示“clouddb deploy failed. Reason is the number of CloudDBZone exceeds the limit.”错误。如AGC云端当前已存在4个存储区，请将数据部署到已有的存储区，或者删除已有存储区后再部署新的存储区。**需要注意的是，删除存储区，该存储区内的数据也将一并删除，且不可恢复。**
- 对象类型中的fieldType等字段信息，部署到AGC云端后，请勿在本地再做修改。例如，fieldType设置为String，对象类型部署成功后，又在本地修改fieldType为Integer，再次部署将失败，提示“clouddb deploy failed. Reason is existing fields cannot be modified.”错误。如需更改fieldType等字段信息，请先删除云端部署的对象类型。**需要注意的是，删除云端对象类型，对象类型内添加的数据也将一并删除，且不可恢复。**

部署云数据库的操作如下：

1. 右击“clouddb”目录，选择“Deploy Cloud DB”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155800.34676704163479890659894143472049:50001231000000:2800:22B81B08C3A11AEE9F856198B8B67E27AF587092C3275584A09638C47DD40C08.png)
    
2. 您可在底部状态栏右侧查看云数据库打包与部署进度。
    
    请您耐心等待，直至出现“Deploy successfully”消息，表示云数据库已成功部署。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155800.66007125660008946514061289920162:50001231000000:2800:436A993F8FCF103BEEAC52A4BD06B84D7250D2AD926B3004520293B604D01D9B.png)
    
    注意
    
    云数据库部署成功后，DevEco Studio将自动从云侧下载云数据库的schema文件至“AppScope/resources/rawfile/schema.json”路径，该文件是云数据库端侧API必须引入的配置文件。
    
    如果后续又在本地工程修改了对象类型，请重新部署云数据库，DevEco Studio将自动更新schema.json文件；如果后续在AGC云侧修改了对象类型，您需[手动从AGC控制台导出schema.json文件](https://developer.huawei.com/consumer/cn/doc/AppGallery-connect-Guides/agc-clouddb-agcconsole-objecttypes-0000001127675459#section1558018208151)，拷贝至本地工程的“AppScope/resources/rawfile”目录下。否则，可能导致schema.json文件中的对象类型和代码中的对象类型不一致，端侧访问云数据库时提示[1008230002](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/cloudfoundation-arkts-error-code#section1432118584210)错误。
    
3. 在菜单栏选择“Tools > CloudDev”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155800.15608213267029042845068461922650:50001231000000:2800:F8507848983B52F60307069DCEB8762D3BEA47D3D36278511B3CEE2CDD7D5E69.png)
    
4. 在打开的CloudDev面板中，点击“Serverless > Cloud DB”下的“Go to console”，进入当前项目的云数据库服务页面。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155800.83125664121720453010161715027078:50001231000000:2800:F63E11341F83E19AC79142F908432F962D0023C0FB124C7E58C63F0675B57E7A.png)
    
5. 分别点击“对象类型”、“存储区”与“数据”页签，可查看到本地开发的云数据库资源均已成功部署至AGC云端。
    
    部署成功后，您便可以从端侧访问云数据库了，具体请参见[在端侧访问云数据库](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-invokeclouddatabase)。
    
    您还可以在AGC控制台继续编辑以上部署的云数据库资源，具体操作请参考[管理数据库](https://developer.huawei.com/consumer/cn/doc/AppGallery-connect-Guides/agc-clouddb-managingclouddb-0000001080815650)。
    
    对象类型“Post”与“objecttype1”：
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155800.13081383994200009104191561071506:50001231000000:2800:ABE2DEE469E703287626D908E0866B6DE2259CF53B624DE666F1F3742849C602.png)
    
    对象类型“Post”所属存储区“Demo”、“objecttype1”所属存储区“cloudDBZoneName1”：
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155800.05883793100800935071076355099639:50001231000000:2800:259EEB174CCA671ACF98822FAB00071DB131488C5A1A21A1A11A5778224B9F66.png)
    
    “d_Post.json”内的数据条目、“d_objecttype1.json”内的数据条目：
    
    说明
    
    部署对象类型或数据条目JSON文件，实际是部署JSON文件内包含的对象类型或数据条目。因此，您在AGC控制台查看到的将是一个个对象类型或者一条条数据，而非JSON文件。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155801.74201683337679074145438121253887:50001231000000:2800:49C737A5D429C933C6D3609215B84F015598C8B4BAFA18534C493F8E5686DA4F.png)
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155801.52961396571359547942510216892512:50001231000000:2800:DB6CF62B6CFECF4F381596B0B678B43CF9D0EDF37267940CC21D33C458504F10.png)
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-dataentry "添加数据条目")
# (可选）一键生成Model Class

更新时间: 2025-12-16 15:58

云数据库支持从端侧或者云侧云函数（含云对象）访问云数据库，代码涉及调用云数据库时，需引入对应云数据库对象类型的Model Class。DevEco Studio当前支持为对象类型一键生成Server Model与Client Model，供您在端侧及云侧云函数（含云对象）开发时引用。

## 生成Server Model

1. 右击需要调用的对象类型文件（以“Post.json”为例），选择“Generate Server Model”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155801.86869674119496787414192991284166:50001231000000:2800:B6F2BB9ABB33278F7747A4A3D3940D9C994E14E8149904A1095163D14AC36A6C.png)
    
2. 选择生成的Server Model文件存放的云函数目录，以“id-generator”为例。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155802.74481074432222058084572556931908:50001231000000:2800:DE662CD56FA7ED86C85BCB65036E6E9792852DADEC7893135CF52EB978CEB852.png)
    
3. 点击“OK”。
    
    指定目录下生成对应对象类型的Server Model文件，后续您便可以在代码中方便地引用该Server Model 。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155802.91118006916606623199676850031687:50001231000000:2800:0D64FC6BB7727181E5F2E7282DBD5C8C409767D22DEFB59813BDBCAEEAEF5EDA.png)
    
4. 在云对象“id-generator”目录的package.json文件中引入@hw-agconnect/cloud-server依赖。
    
    1. "dependencies": {
    2.   "@hw-agconnect/cloud-server": "latest"
    3. }
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155802.85432452670133910359155684028149:50001231000000:2800:66BCA54BB1781F25C716C3587ABF20B87186D48640CB50CB88D7547E2A5156D3.png)
    
5. 在云对象文件idGenerator.ts中添加如下代码，实现云函数访问云数据库。
    
    1. import { cloud } from '@hw-agconnect/cloud-server'; 
    2. import { Post } from './Post'; // Post是Server Model 
    
    3. // Demo是Post对象类型使用的存储区名
    4. const collection = cloud.database({ zoneName: 'Demo' }).collection(Post);
    
    5. // IdGenerator云对象，实现了对Post对象类型的查询和更新
    6. export class IdGenerator {
    7.   query() {
    8.     return collection.query().get();
    9.   }
    
    10.   upsert(posts: Post[]) {
    11.     return new Promise((resolve, reject) => {
    12.       collection.upsert(posts.map(post => Post.parseFrom(post)))
    13.         .then(result => resolve({ result }))
    14.         .catch(err => reject(err))
    15.     });
    16.   }
    17. }
    
    注意
    
    如果定义的云数据库表字段中包含ByteArray或Date类型的字段，在插入或者更新云数据库时需要使用Server Model的parseFrom方法将入参转化成API识别的类型，例如上述示例中的Post.parseFrom方法。
    

## 生成Client Model

1. 右击需要调用的对象类型文件（以“Post.json”为例），选择“Generate Client Model”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155802.25247514119891482748826265550536:50001231000000:2800:879C363A544AF1946E72AD4105EF42AAD9B9E75FAC9050B09532388464B4DF1D.png)
    
2. 选择生成的Client Model文件存放的端侧目录。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155802.11512568355852907624329005995365:50001231000000:2800:E6BA6866F5C76CB59C5604E29AD2868EAD47485C9CCC1E6B77A3CA52A8AD7DF8.png)
    
3. 点击“OK”。
    
    指定目录下生成对应对象类型的Client Model文件，后续您便可以在端侧代码中方便地引用该Client Model，具体可参考端云一体化工程初始化代码中的Client Model示例（“ets/pages/CloudDb/Post.ts”）在CloudDb.ets以及DbInset.ets中的引用。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155802.81838238711183206552921154186620:50001231000000:2800:DBC91F053E569A6C764D125664C06C7042485C8D50C6F6A7614D5DD4688A3D52.png)
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-deploydatabase "部署云数据库")
# 部署云侧工程

更新时间: 2025-12-16 15:57

您也可选择在云函数和云数据库全部开发完成后，将整个云工程资源统一部署到AGC云端。

1. 右击云开发工程（“CloudProgram”），选择“Deploy Cloud Program”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155737.75677703580197461899705327271381:50001231000000:2800:E43996C817D7C1CB73733479CBD4EAAFF349849586A7D5AA905861D6298FC214.png)
    
2. 您可在底部状态栏右侧查看云工程打包与部署进度。
    
    请您耐心等待，直至出现“Deploy successfully”消息，表示云工程已成功部署。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155737.45770238263650785792997819326721:50001231000000:2800:776B6D4F5ACF984DA29D22E85625B505E376C48A643EE59E87BDE3E1000A1CC8.png)
    
3. 在菜单栏选择“Tools > CloudDev”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155737.16074850446835241365573509784954:50001231000000:2800:7289A41D4ECA634B8AF4C8F01DB4D2AB10F9BB172CB71BD76C98FB1C9B151C7C.png)
    
4. 在打开的CloudDev面板中，点击“Go to console”，打开当前项目的AGC Serverless子控制台。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155737.54646952398044425375261739635982:50001231000000:2800:269A1A14DF47328CDB8B5A29A1E7475B9E9528517E511D71E371473352F73948.png)
    
5. 分别进入云函数与云数据库服务菜单，可查看到您刚刚部署的云函数与云数据库资源。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155737.91538776856722868467056655894069:50001231000000:2800:1E3CE7DBF8658F37F4D196B5047023DB267164707A4FD4B3A82F9A09479A2620.png)
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-modelclass "(可选）一键生成Model Class")
# （可选）同步云端代码至DevEco Studio工程

更新时间: 2025-12-16 15:57

DevEco Studio还支持您将AGC云端当前项目下的代码同步至本地工程，包括之前从本地部署到AGC云端的代码、以及在AGC云端编写的代码，以保证云端和本地的版本一致性，方便您的日常开发。

云端代码同步目前支持以下模式：[仅同步云函数/云对象](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-sync#section588213529814)、[仅同步云数据库](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-sync#section474014335350)、[一键同步云侧代码](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-sync#section1198316575339)。

## 同步云函数/云对象

说明

对于使用DevEco Studio 4.1 Canary 2之前的版本部署的函数，同步下来的是JavaScript代码。

### 同步单个云函数/云对象

云函数/云对象部署到AGC云端后，如在云端又进行了新改动，您可再将云端的云函数/云对象同步到本地工程。云函数/云对象的同步方式一致，下文以云对象为例进行说明。

1. 右击云对象目录，选择“Sync '_云对象名_'”。下文以云对象“id-generator”为例。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155739.78306657759754180640607933108469:50001231000000:2800:5A06AFA3BCFA15BFEBE910EB976E780EEE4A4D787D23CD1E90E1E545AE2256D7.png)
    
2. 在确认弹框中点击“Overwrite”，AGC云端的云对象“id-generator”将覆盖更新本地云对象“id-generator”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155739.10766181437731481849959359657108:50001231000000:2800:5DB7AA64A2AED00D5B4BEF3B478D15FCF0F2A74A703CF38382AFD87798FC5FF6.png)
    
3. 等待同步完成，“cloudfunctions”目录下将生成从云端同步下来的云对象“id-generator”，同时将本地原云对象“id-generator”备份在同路径下。
    
    说明
    
    后续如执行部署或调试，DevEco Studio会自动跳过备份数据。但出于精简包的考虑，建议您在对比代码差异后，及时将无用的备份数据删除。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155739.02365794747165770445245494266958:50001231000000:2800:8A72CA935ABDE7BD7E207929F13EF019904B0A64C8C83A947C35A76F2A3D55EE.png)
    

### 批量同步云函数/云对象

批量同步云函数/云对象即将AGC云端当前项目下的所有云函数/云对象同步至本地工程。

1. 右击“cloudfunctions”目录，选择“Sync Cloud Functions”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155739.22841819525421179948499607792824:50001231000000:2800:ADD5477B36C43C2BD8A41D16BF440C3B332DBCB3026A90A074BCBF6113E0C509.png)
    
2. 弹窗提示您本地工程下存在同名云函数/云对象。
    
    - 选择“Skip”，同步时将跳过本地同名云函数/云对象。
    - 选择“Overwrite”，AGC云端的云函数/云对象将覆盖更新本地同名云函数/云对象。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155739.82281567942683134010396465555610:50001231000000:2800:C2D3F2A37BDF4C694DA1FD87D57DCD80CD8BA3C0BE9DDE2E8113C52B965427C5.png)
    
3. 如选择“Skip”，等待同步完成后，“cloudfunctions”目录下将生成从云端同步下来的本项目下所有云函数/云对象，本地已存在的不同步。
    
    如下图，“cloudfunctions”目录下新增了云端同步下来的“test-cloud-function”，上图中本地已存在的云函数/云对象未被覆盖更新。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155739.52139666673936494763442986166428:50001231000000:2800:B120697631416B173713491CD4055E2BDACC03A8D7EFD4FE04B845672F1768D9.png)
    
4. 如选择“Overwrite”，等待同步完成后，“cloudfunctions”目录下将生成从云端同步下来的本项目下所有云函数/云对象；本地同名云函数/云对象也被覆盖更新，同时更新前的原云函数/云对象会备份在同路径下。
    
    如下图，“cloudfunctions”目录下新增了云端同步下来的“test-cloud-function”，本地已存在的几个云函数/云对象也被覆盖更新，并且均生成了备份文件“xxxx-_备份时间_.backup”。
    
    说明
    
    后续如执行部署或调试，DevEco Studio会自动跳过备份数据。但出于精简包的考虑，建议您在对比代码差异后，及时将无用的备份数据删除。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155739.70803199746766233358580436781066:50001231000000:2800:354EA82902334DD7D175807161F09449E1295C3A816F924F5B7487D2383EE134.png)
    

## 同步云数据库

说明

目前仅支持同步对象类型。

### 同步单个对象类型

对象类型部署到AGC云端后，如又发生了新改动，您可再将云端的对象类型同步到本地。

1. 右击对象类型JSON文件（以“objecttype1.json”为例），选择“Sync 'objecttype1.json'”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155739.44835823737734152886749442110786:50001231000000:2800:75A0DCC132CB70992696D96034CF69BD2D501339F53F1A51C60E14F007CB22BF.png)
    
2. 在确认弹框中点击“Overwrite”，AGC云端的对象类型“objecttype1.json”将覆盖更新本地对象类型“objecttype1.json”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155740.20890725872933011087230618689504:50001231000000:2800:8523CBDB6CA789F112B17EC4B921A71A4185B0F206F643C702D04F28CBD306A7.png)
    
3. 等待同步完成，“objecttype”目录下将生成从云端同步下来的对象类型“objecttype1.json”。
    
    - 如果云端和本地的同名对象类型内容存在差异，则还会将本地原对象类型备份在同路径下。
    - 如果云端和本地的同名对象类型内容完全一致，则不生成备份。
    
    说明
    
    后续如执行部署，DevEco Studio会自动跳过备份数据。但出于精简包的考虑，建议您在对比代码差异后，及时将无用的备份数据删除。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155740.58407173914326328486418935287044:50001231000000:2800:5DF089F6A2B9566D03FEF65F5BC3C9AD7407EF277AA1336F985C1F9ABC3C383E.png)
    

### 批量同步对象类型

您可以将AGC云端当前项目下所有的对象类型一键同步至本地。

1. 右击“objecttype”目录，选择“Sync Object Type”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155740.04222927459390116870570881429753:50001231000000:2800:F093615167510E892F4862DAA2A85689EA216838AF5ED5D3F84C850326FB88D2.png)
    

2. 弹窗提示您本地工程下已存在同名对象类型，如下图“Post.json”与“objecttype1.json”。
    
    - 选择“Skip”，同步时将跳过本地同名对象类型。
    - 选择“Overwrite”，AGC云端的对象类型将覆盖更新本地同名对象类型。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155740.07367360475078574405942092990938:50001231000000:2800:7AFBECFDEF6CE7D7672FAFBB9009A651DA451DAD4235FD49C39E01FA30558F07.png)
    
3. 如选择“Skip”，等待同步完成后，“objecttype”目录下将生成从云端同步下来的本项目下所有对象类型，本地已存在的不同步。
    
    如下图，“objecttype”目录下新增了云端同步下来的“test_object.json”，本地已存在的“Post.json”与“objecttype1.json”未被覆盖更新。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155740.46304442012929923216285732227876:50001231000000:2800:532B5B0A91B8D067CAC0F786C632FF9523DE383A2F47351165D649B17E2F1725.png)
    
4. 如选择“Overwrite”，等待同步完成后，“objecttype”目录下将生成从云端同步下来的所有对象类型，本地已存在的对象类型也被覆盖更新。
    
    - 如果云端和本地的同名对象类型内容存在差异，则还会将本地原对象类型备份在同路径下。
    - 如果云端和本地的同名对象类型内容完全一致，则不生成备份。
    
    如下图，“objecttype”目录下生成了“test_object.json”、“Post.json”与“objecttype1.json”三个对象类型文件，其中：“test_object.json”为从云端新同步下来的对象类型；“objecttype1.json”本地已存在且与云端内容一致，不生成备份；“Post.json”本地已存在但与云端内容存在差异，因此被覆盖更新，同时原“Post.json”备份为“Post.json-_备份时间_.backup”。
    
    说明
    
    后续如执行部署，DevEco Studio会自动跳过备份数据。但出于精简包的考虑，建议您在对比代码差异后，及时将无用的备份数据删除。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155740.15410285680879497100762895184494:50001231000000:2800:A895961AD7A945B1352F65B817C3409E27F3D996B4C0479E935F95D972FC113F.png)
    

## 一键同步云侧代码

说明

对于使用DevEco Studio 4.1 Canary 2之前的版本部署的函数，同步下来的是JavaScript代码。

1. 右击云开发工程（“CloudProgram”），选择“Sync Cloud Program”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155740.45215109214398119302100250113995:50001231000000:2800:AA6B99C0C9E5C967E4880E18FFB2BEB6B40F62AD0224E8942D0FCFA2ABCE4D73.png)
    
2. 弹窗提示您本地工程下已存在同名对象类型/云函数/云对象。
    
    - 选择“Skip”，同步时将跳过本地同名对象类型/云函数/云对象。
    - 选择“Overwrite”，AGC云端的对象类型/云函数/云对象将覆盖更新本地同名对象类型/云函数/云对象。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155740.56975866599072467655897348898457:50001231000000:2800:D2B642D1FDF1CBD6932DE6DAE115CBF9B7EADD9DA6BBAFF5518676DF309F05B4.png)
    
3. 如选择“Skip”，等待同步完成后，“objecttype”目录下将生成从云端同步下来的本项目下所有对象类型，“cloudfunctions”目录下将生成从云端同步下来的本项目下所有云函数/云对象，本地已存在的云函数/云对象/对象类型均不同步。
    
    如下图：
    
    - “objecttype”目录下新增了云端同步下来的“test_object.json”，本地已存在的“Post.json”与“objecttype1.json”未被覆盖更新。
    - “cloudfunctions”目录下生成了从云端同步下来的“test-cloud-function”，本地已存在的“id-generator”、“my-cloud-function”与“my-cloud-object”未被覆盖更新。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155740.99593665535224015444537984658957:50001231000000:2800:FF9040F11DE40872E6EA4D0C315CF1EE1350BD940C898C78B2C59DEED1485807.png)
    
4. 如选择“Overwrite”，等待同步完成后，“objecttype”目录下将生成从云端同步下来的本项目下所有对象类型，“cloudfunctions”目录下将生成从云端同步下来的本项目下所有云函数/云对象，本地已存在的云函数/云对象/对象类型也被覆盖更新。
    
    - 如果云端和本地的同名对象类型内容存在差异，则还会将本地原对象类型备份在同路径下。
    - 如果云端和本地的同名对象类型内容完全一致，则不生成备份。
    - 无论云端和本地的同名云函数/云对象代码是否一致，均会将本地原云函数/云对象备份在同路径下。
    
    如下图：
    
    - “objecttype”目录下生成了“test _object.json”、“Post.json”与“objecttype1.json”三个对象类型文件，其中：“test _object.json”为从云端新同步下来的对象类型；“Post.json”本地已存在且与云端内容一致，不生成备份；“objecttype1.json”本地已存在但与云端内容存在差异，因此被覆盖更新，同时原“objecttype1.json”备份为“objecttype1.json-_备份时间_.backup”。
    - “cloudfunctions”目录下生成了从云端同步下来的“test-cloud-function”，本地已存在的“id-generator”、“my-cloud-function”与“my-cloud-object”也被覆盖更新，并且均生成了备份文件“xxxx-_备份时间_.backup”。
        
        说明
        
        后续如执行部署或调试，DevEco Studio会自动跳过备份数据。但出于精简包的考虑，建议您在对比代码差异后，及时将无用的备份数据删除。
        
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155740.85271874922980510160118098289709:50001231000000:2800:FB1404CE755365CADA73EC8B77CCBC6E90E2F68F698796497DA154CA266D7E4E.png)
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-deploy "部署云侧工程")
# 在端侧调用云函数

更新时间: 2025-12-16 15:57

## 前提条件

请确保[云函数已正确开发并部署](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-deployfunc)。

## 操作步骤

1. 在代码文件中引入Cloud Foundation Kit。
    
    1. import { cloudFunction } from '@kit.CloudFoundationKit'
    2. import { BusinessError } from '@kit.BasicServicesKit';
    
2. 调用您云侧部署的云函数。关于云函数接口的更详细信息，请参考[Cloud Foundation Kit API参考-云函数模块](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/cloudfoundation-cloudfunction)。
    
    1. //填入需要调用的云函数名称
    2. cloudFunction.call({name: 'xxxx'})
    3. .then((res: cloudFunction.FunctionResult) => {  
    4.   // 处理调用返回
    5. }).catch((err: BusinessError) => {
    6.   // 调用云函数异常时的处理逻辑
    7. })
    
    例如，调用云侧函数“my-cloud-function”，以返回一个时间戳。
    
    8. import { cloudFunction } from '@kit.CloudFoundationKit';
    9. import { BusinessError } from '@kit.BasicServicesKit';
    
    10. interface result {
    11.   intervalTime: number
    12. }
    
    13. interface res {
    14.   result: result
    15. }
    
    16. @Entry
    17. @Component
    18. struct CloudFunction {
    19.   @State globalId: string = '';
    
    20.   build() {
    21.     Column() {
    22.       Navigation()
    23.         .title($r('app.string.cloud_function_title'))
    24.         .height('50vp')
    25.         .width('100%')
    26.         .margin({ bottom: 10 })
    27.         .titleMode(NavigationTitleMode.Mini)
    
    28.       Text($r('app.string.cloud_function_description'))
    29.         .width('90%')
    30.         .textAlign(TextAlign.Center)
    31.         .margin({ top: 20, bottom: 20 })
    32.         .fontSize($r('app.float.body_font_size'))
    33.       Button({ type: ButtonType.Normal }) {
    34.         Text($r('app.string.cloud_function_button_text'))
    35.           .fontColor($r('app.color.white'))
    36.           .margin({ top: 5, bottom: 5 })
    37.       }
    38.       .width('90%')
    39.       .borderRadius('8vp')
    40.       .height('30vp')
    41.       .margin({ top: 10 })
    42.       .onClick(() => {
    43.         this.callMyFunction()
    44.       })
    
    45.       Column() {
    46.         Text(this.globalId).fontSize($r('app.float.body_font_size'))
    47.       }
    48.       .width('90%')
    49.       .padding({ top: 20, bottom: 20 })
    50.       .margin({ top: 20 })
    51.       .backgroundColor($r('app.color.placeholder_background'))
    52.     }.height('100%')
    53.   }
    
    54.   callMyFunction() {
    55.     cloudFunction.call({ name: 'my-cloud-function' }).then((res: cloudFunction.FunctionResult) => {
    56.       let callback  = res as res;
    57.       console.info(`Succeeded in call the function, time:${callback.result.intervalTime} `);
    58.     }).catch((err: BusinessError) => {
    59.       console.error(`Failed to call the function, Code: ${err.code}, message: ${err.message}`);
    60.     });
    61.   }
    62. }
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-invokecloudcode "在端侧调用云侧代码")
# 在端侧调用云对象

更新时间: 2025-12-16 15:57

云对象开发完成后，您可以为其生成端侧调用接口类，供后续端侧工程调用云对象使用。

## 前提条件

请确保[云对象已正确开发并部署](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-deploycloudobj)。

## 操作步骤

1. 右击云对象（以“my-cloud-object”为例），选择“Generate Invoke Interface”。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155756.62344788317802621312127439940215:50001231000000:2800:D6A25F959928C3DD2B6EB888E81FA2D642CF642D05A658D1127C4F062E754E17.png)
    
2. 在弹出的“Generate Invoke Interface”窗口，可以看到生成的端侧调用接口类将默认存储在“Application/cloud_objects”模块目录下，点击“OK”确认。您也可以点击“...”按钮自定义存储目录。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155756.88366125139889401220342366681953:50001231000000:2800:AAA6ADFF1F500287D6D0CEDFEE4A511B7F67EDC2F51119D4AD940261080E097F.png)
    
3. DevEco Studio自动打开指定的端侧调用接口类存储目录，该目录包含“ImportObject.ts”文件和“my-cloud-object”文件夹。
    
    - “ImportObject.ts”文件定义了importObject方法，可以通过该方法来实例化一个云对象的代理。
    - “my-cloud-object”文件夹包含了该云对象在端侧可能用到的所有模型。示例中只有一个“MyCloudObject.ts”文件，如果有其它的模型也将生成在该文件夹下。
    - “MyCloudObject.ts”文件中定义了MyCloudObject class，并且定义了add和subtract两个方法。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155756.21666741433035592674204887364104:50001231000000:2800:3D09CAFA79E8CFA82E78E156A0156EC6D29482DA5F95F7597AEDCF698432D159.png)
    
4. 在代码文件中引入云对象。
    
    1. import { MyCloudObject, importObject } from 'cloud_objects';
    
5. 调用云对象中的方法。
    
    1. let myCloudObject = importObject(MyCloudObject); // 使用importObject实例化MyCloudObject的代理
    2. myCloudObject.add(1, 2).then(addResult => {
    3.   console.log(`1 + 2 = ${addResult.result}`);
    4. }); // 忽略异常处理
    5. myCloudObject.subtract(6, 3).then(subtractResult => {
    6.   console.log(`6 - 3 = ${subtractResult.result}`);
    7. });
    
    由于“Generate Invoke Interface”时已经生成所需要的模型以及importObject方法，因此在编码时可以很方便地使用联想、自动引入等DevEco Studio提供的高阶能力，如下图所示。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155756.11124472319339006864267560909114:50001231000000:2800:48016B9BE9C76B7E77F939D13C5FBEF4BF590F2F6F68A1CAFFB42699647372E8.png)
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-invokecloudfunc "在端侧调用云函数")
# 在端侧访问云数据库

更新时间: 2025-12-16 15:57

## 前提条件

- 请确保[云数据库已正确开发并部署](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-deploydatabase)。
- 请确保“AppScope/resources/rawfile/schema.json”文件已存在。
    
    注意
    
    云数据库部署成功后，DevEco Studio将自动从云侧下载云数据库的schema文件至“AppScope/resources/rawfile/schema.json”路径，该文件是云数据库端侧API必须引入的配置文件。
    
    如果后续又在本地工程修改了对象类型，请重新部署云数据库，DevEco Studio将自动更新schema.json文件；如果后续在AGC云侧修改了对象类型，您需[手动从AGC控制台导出schema.json文件](https://developer.huawei.com/consumer/cn/doc/AppGallery-connect-Guides/agc-clouddb-agcconsole-objecttypes-0000001127675459#section1558018208151)，拷贝至本地工程的“AppScope/resources/rawfile”目录下。否则，可能导致schema.json文件中的对象类型和代码中的对象类型不一致，端侧访问云数据库时提示[1008230002](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/cloudfoundation-arkts-error-code#section1432118584210)错误。
    

- 检查您的角色拥有的对象类型操作权限。如果未[配置AccessToken](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/cloudfoundation-cloudcommon#section9723191765120)，需要给World角色添加Upsert和Delete权限。

## 生成Client Model

在端侧通过Cloud Foundation Kit访问云数据库，需先引入对应云数据库对象类型的Client Model。

参考[生成Client Model](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-modelclass#section1037851593420)生成云数据库对象类型的端侧模型，如下图初始化代码中的Client Model示例“ets/pages/CloudDb/Post.ts”。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216155758.52000665261267637365828015080354:50001231000000:2800:8B44503903F8D46CA624492B3721777D1DDABC396B9F48E7B3B13055E38618A0.png)

## 访问数据库

接下来您便可参考[初始化数据库访问](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-database-initialize)、[查询数据](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-database-query)、[写入数据](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-database-upsert)、[删除数据](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/cloudfoundation-database-delete)等访问数据库。

“src/main/ets/pages/CloudDb”目录下提供了部分示例代码，更完整的接口信息请参考[Cloud Foundation Kit API参考-云数据库模块](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/cloudfoundation-clouddatabase)。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-invokecloudobj "在端侧调用云对象")
# 在端侧调用云存储

更新时间: 2025-12-16 15:58

## 前提条件

- 请确保云存储服务已经开通。
- 使用云存储功能，需要获取用户凭据。请确保您已[配置AccessToken](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/cloudfoundation-cloudcommon#section9723191765120)。

## 操作步骤

1. 在代码文件中引入Cloud Foundation Kit。
    
    1. import { cloudStorage } from '@kit.CloudFoundationKit';
    2. import { BusinessError, request } from '@kit.BasicServicesKit';
    
2. 初始化云存储实例。
    
    1. const bucket: cloudStorage.StorageBucket = cloudStorage.bucket();
    
3. 调用云存储接口，如uploadFile接口。“src/main/ets/pages/CloudStorage.ets”代码片段节选如下，更完整的接口信息请参考[Cloud Foundation Kit API参考-云存储模块](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/cloudfoundation-cloudstorage)。
    
    1. bucket.uploadFile(getContext(this), {
    2.   localPath: cacheFilePath,
    3.   cloudPath: cloudPath,
    4. }).then(task => {
    5.   // add task event listener
    6.   this.addEventListener(task, this.onUploadCompleted(cloudPath, cacheFilePath));
    7.   // start task
    8.   task.start();
    9. }).catch((err: BusinessError) => {
    10.   hilog.error(HILOG_DOMAIN, TAG, 'uploadFile failed, error code: %{public}d, message: %{public}s',
    11.     err.code, err.message);
    12.   this.isUploading = false;
    13. });
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/agc-harmonyos-clouddev-invokeclouddatabase "在端侧访问云数据库")
