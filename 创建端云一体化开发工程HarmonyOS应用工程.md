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
