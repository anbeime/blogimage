# Calendar Kit简介

更新时间: 2025-12-16 16:35

Calendar Kit（日历服务）提供日历与日程管理能力，通常是指可以用于访问和操作日历数据的API（应用程序接口）。这些接口允许开发者将其他应用中的工作、生活中与时间相关的日程服务（如出行、餐饮、运动、娱乐等）与系统日历进行集成，从而实现日程管理、事件创建、查询等功能。

## 能力范围

Calendar Kit包括账户管理和日程管理。

- 创建日历账户。
    
    开发者可以创建属于本应用特有的日历账户，账户创建成功后会返回一个账户id，账户id是数据表自增主键，作为账户的唯一标识符。
    
- 获取日历账户。
    
    开发者可以获取指定的日历账户信息或者获取当前应用创建的所有日历账户信息。
    
- 删除日历账户。
    
    开发者可以删除指定的日历账户，日历账户删除后，和该日历账户所关联的全部日程都会被删除。
    
- 创建日程。
    
    开发者获取到日历账号信息后，可以在获取到的日历账户下创建日程。创建日程时可以设置日程提醒时间，到达日程提醒时间时会有日程提醒通知弹出。
    
    日程创建成功后会返回一个日程id，日程id是数据表自增主键，作为日程的唯一标识符。
    
- 删除日程。
    
    开发者可以指定日程id进行日程的删除，可以同时删除一条或者多条日程。
    
- 更新日程。
    
    开发者可以根据日程id对日程信息进行更新，包括更新日程标题、日程地点、日程开始时间、日程结束时间、日程提醒时间等信息。
    
- 查询日程。
    
    查询日程支持三种方式：根据日程id查询日程、根据日程标题查询日程、根据日程的开始时间和结束时间查询日程。
    

## 亮点/特征

**日程一键服务**：开发者通过永久性授权机制，在用户许可当前应用读写系统日历后，可将对应的日程服务以DeepLink的形式同时写入日历。根据开发者设置的提醒规则，在日程临近或到期时，日历应用、日历通知、日历卡片等区域同时会显示对应的“服务按钮”，用户可通过点击此按钮拉起跳转链接，一步直达服务落地页。

## 运作机制

Calendar Kit为用户提供了一系列接口来获取日历账户，并使用特定的接口向日历账户中写入或读取日程信息。如果写入的日程带有提醒时间则系统会在时间到达时向用户发送提醒。

## 约束限制

- 目前Calendar Kit的相关能力及接口使用，仅支持在Stage模型下使用。
    
- 使用Calendar Kit的相关能力，需要获取读取或写入日历、日程的权限。具体指导可见[声明权限](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/declare-permissions)。
    
    - 进行日历或日程的读取时，需要申请ohos.permission.READ_CALENDAR或ohos.permission.READ_WHOLE_CALENDAR权限。
        
    - 进行日历或日程的添加、删除或修改时，需要申请ohos.permission.WRITE_CALENDAR或ohos.permission.WRITE_WHOLE_CALENDAR权限。
        
    
    申请对应权限之后，支持的相关操作可见下表。
    
    |申请的权限|支持的日历账户操作范围|支持的日程操作范围|
    |:--|:--|:--|
    |ohos.permission.READ_CALENDAR|- 读取系统默认日历账户<br><br>- 读取当前应用创建的日历账户|- 读取系统默认日历账户下当前应用创建的日程<br><br>- 读取当前应用创建的日历账户下当前应用创建的日程|
    |ohos.permission.WRITE_CALENDAR|- 添加、删除或修改当前应用创建的日历账户|- 添加、删除或修改系统默认日历账户下当前应用创建的日程<br><br>- 添加、删除或修改当前应用创建的日历账户下当前应用创建的日程|
    |ohos.permission.READ_WHOLE_CALENDAR|- 读取所有日历账户|- 读取所有应用创建的日程|
    |ohos.permission.WRITE_WHOLE_CALENDAR|- 添加、删除或修改所有日历账户|- 添加、删除或修改所有应用创建的日程|
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/calendar-kit "Calendar Kit（日历服务）")
# 日历账户管理

更新时间: 2025-12-16 16:36

日历账户‌用于存储和管理个人或团队的日程，通过日历账户，用户可以方便地查看、编辑和共享日程信息。

日历管理器[CalendarManager](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-calendarmanager#calendarmanager)用于管理日历账户[Calendar](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-calendarmanager#calendar)。日历账户主要包含账户信息[CalendarAccount](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-calendarmanager#calendaraccount)和配置信息[CalendarConfig](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-calendarmanager#calendarconfig)。

开发者可以创建属于应用特有的日历账户，还可以对日历账户进行新增、删除、更新和查询。此外，每个日程[Event](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-calendarmanager#event)归属于某一个特定的日历账户，可以通过日历账户对该账户下面的日程进行管理，具体相关指导可见[日程管理](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/calendarmanager-event-developer)。

## 接口说明

以下是日历账户管理的相关接口，更多详细接口及使用请参考[@ohos.calendarManager](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-calendarmanager)。

|接口名称|描述|
|:--|:--|
|getCalendarManager(context: Context): CalendarManager|根据上下文获取日历管理器对象CalendarManager，用于管理日历。|
|createCalendar(calendarAccount: CalendarAccount): Promise<Calendar>|根据日历账户信息，创建一个Calendar对象，使用Promise异步回调。|
|getCalendar(calendarAccount?: CalendarAccount): Promise<Calendar>|获取默认Calendar对象或者指定Calendar对象，使用Promise异步回调。<br><br>默认Calendar是日历存储首次运行时创建的，若创建Event时不关注其Calendar归属，则无须通过createCalendar()创建Calendar，直接使用默认Calendar。|
|getAllCalendars(): Promise<Calendar[]>|获取当前应用所有创建的Calendar对象以及默认Calendar对象，使用Promise异步回调。|
|deleteCalendar(calendar: Calendar): Promise<void>|删除指定Calendar对象，使用Promise异步回调。|
|getConfig(): CalendarConfig|获取日历配置信息。|
|setConfig(config: CalendarConfig): Promise<void>|设置日历配置信息，使用Promise异步回调。|
|getAccount(): CalendarAccount|获取日历账户信息。|

## 开发步骤

1. 导入相关依赖。
    
    1. // EntryAbility.ets
    2. import { abilityAccessCtrl, AbilityConstant, common, PermissionRequestResult, Permissions, UIAbility, Want } from '@kit.AbilityKit';
    3. import { BusinessError } from '@kit.BasicServicesKit';
    4. import { calendarManager } from '@kit.CalendarKit';
    5. import { window } from '@kit.ArkUI';
    
2. 申请权限。使用Calendar Kit时，需要在module.json5中声明申请读写日历日程所需的权限：ohos.permission.READ_CALENDAR和ohos.permission.WRITE_CALENDAR。具体指导可见[声明权限](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/declare-permissions)。
    
3. 根据上下文获取日程管理器对象calendarMgr，用于对日历账户进行相关管理操作。推荐在EntryAbility.ets文件中进行操作。
    
    1. // EntryAbility.ets
    2. export let calendarMgr: calendarManager.CalendarManager | null = null;
    
    3. export let mContext: common.UIAbilityContext | null = null;
    
    4. export default class EntryAbility extends UIAbility {
    5.   onCreate(want: Want, launchParam: AbilityConstant.LaunchParam): void {
    6.     console.info("Ability onCreate");
    7.   }
    
    8.   onDestroy(): void {
    9.     console.info("Ability onDestroy");
    10.   }
    
    11.   onWindowStageCreate(windowStage: window.WindowStage): void {
    12.     // Main window is created, set main page for this ability
    13.     console.info("Ability onWindowStageCreate");
    14.     windowStage.loadContent('pages/Index', (err, data) => {
    15.       if (err.code) {
    16.         console.error(`Failed to load the content. Code: ${err.code}, message: ${err.message}`);
    17.         return;
    18.       }
    19.       console.info(`Succeeded in loading the content. Data: ${JSON.stringify(data)}`);
    20.     });
    21.     mContext = this.context;
    22.     const permissions: Permissions[] = ['ohos.permission.READ_CALENDAR', 'ohos.permission.WRITE_CALENDAR'];
    23.     let atManager = abilityAccessCtrl.createAtManager();
    24.     atManager.requestPermissionsFromUser(mContext, permissions).then((result: PermissionRequestResult) => {
    25.       console.info(`get Permission success, result: ${JSON.stringify(result)}`);
    26.       calendarMgr = calendarManager.getCalendarManager(mContext);
    27.     }).catch((error: BusinessError) => {
    28.       console.error(`get Permission error, error. Code: ${error.code}, message: ${error.message}`);
    29.     })
    30.   }
    
    31.   onWindowStageDestroy(): void {
    32.     // Main window is destroyed, release UI related resources
    33.     console.info("Ability onWindowStageDestroy");
    34.   }
    
    35.   onForeground(): void {
    36.     // Ability has brought to foreground
    37.     console.info("Ability onForeground");
    38.   }
    
    39.   onBackground(): void {
    40.     // Ability has back to background
    41.     console.info("Ability onBackground");
    42.   }
    43. }
    
4. 根据日历账户信息，创建一个日历账户Calendar对象。
    
    创建日历账户之前，开发者需要先根据账户信息进行查询，如果账户不存在则抛出异常信息，捕获到异常再进行日历账户的创建，否则可能会出现账户重复创建的问题。
    
    1. // Index.ets
    2. import { BusinessError } from '@kit.BasicServicesKit';
    3. import { calendarMgr } from '../entryability/EntryAbility';
    4. import { calendarManager } from '@kit.CalendarKit';
    
    5. let calendar: calendarManager.Calendar | undefined = undefined;
    6. // 指定日历账户信息
    7. const calendarAccount: calendarManager.CalendarAccount = {
    8.   // 日历账户名称
    9.   name: 'MyCalendar',
    10.   // 日历账户类型
    11.   type: calendarManager.CalendarType.LOCAL,
    12.   // 日历账户显示名称，该字段如果不填，创建的日历账户在界面显示为空字符串。
    13.   displayName: 'MyCalendar'
    14. };
    15. // 创建日历账户
    16. calendarMgr?.createCalendar(calendarAccount).then((data: calendarManager.Calendar) => {
    17.   console.info(`Succeeded in creating calendar data->${JSON.stringify(data)}`);
    18.   calendar = data;
    19.   // 请确保日历账户创建成功后，再进行后续相关操作
    20.   // ...
    21. }).catch((error: BusinessError) => {
    22.   console.error(`Failed to create calendar. Code: ${error.code}, message: ${error.message}`);
    23. });
    
5. 日历账户创建之后，日历账户颜色默认为黑色，不指定日历账户颜色可能导致部分版本/设备深色模式下显示效果不佳。开发者需要调用setConfig()接口设置日历配置信息，包括是否打开日历账户下的日程提醒能力、设置日历账户颜色。
    
    1. // Index.ets
    2. const calendarAccounts: calendarManager.CalendarAccount = {
    3.   name: 'MyCalendar',
    4.   type: calendarManager.CalendarType.LOCAL,
    5.   displayName: 'MyCalendar'
    6. };
    7. // 日历配置信息
    8. calendarMgr?.getCalendar(calendarAccounts, (err, data) => {
    9.   //获取日历账户
    10.   if (err) {
    11.     console.error(`Failed to get calendar, Code is ${err.code}, message is ${err.message}`);
    12.   } else {
    13.     const config: calendarManager.CalendarConfig = {
    14.       // 打开日程提醒
    15.       enableReminder: true,
    16.       // 设置日历账户颜色
    17.       color: '#aabbcc'
    18.     };
    19.     // 设置日历配置信息
    20.     data.setConfig(config).then(() => {
    21.       console.info(`Succeeded in setting config, data->${JSON.stringify(config)}`);
    22.     }).catch((err: BusinessError) => {
    23.       console.error(`Failed to set config. Code: ${err.code}, message: ${err.message}`);
    24.     })
    25.   }
    26. });
    
6. 可以查询指定日历账户。
    
    1. // Index.ets
    2. calendarMgr?.getCalendar(calendarAccount).then((data: calendarManager.Calendar) => {
    3.  console.info(`Succeeded in getting calendar, data -> ${JSON.stringify(data)}`);
    4. }).catch((err: BusinessError) => {
    5.  console.error(`Failed to get calendar. Code: ${err.code}, message: ${err.message}`);
    6. });
    
7. 也可以查询默认日历账户，默认日历账户是日历存储首次运行时创建的，若创建日程时不关注归属哪个账户，则无须单独创建日历账户，可以直接使用默认日历账户。
    
    1. // Index.ets
    2. calendarMgr?.getCalendar().then((data: calendarManager.Calendar) => {
    3.  console.info(`Succeeded in getting calendar, data -> ${JSON.stringify(data)}`);
    4. }).catch((err: BusinessError) => {
    5.  console.error(`Failed to get calendar. Code: ${err.code}, message: ${err.message}`);
    6. });
    
8. 获取当前应用所有创建的日历账户及默认日历账户Calendar对象。
    
    由于涉及数据隐私安全，进行了权限管控的应用无法获取其他应用创建的账户信息。
    
    1. // Index.ets
    2. calendarMgr?.getAllCalendars().then((data: calendarManager.Calendar[]) => {
    3.   console.info(`Succeeded in getting all calendars, data -> ${JSON.stringify(data)}`);
    4.   data.forEach((calendar) => {
    5.     const account = calendar.getAccount();
    6.     console.info(`account -> ${JSON.stringify(account)}`);
    7.   })
    8. }).catch((err: BusinessError) => {
    9.   console.error(`Failed to get all calendars. Code: ${err.code}, message: ${err.message}`);
    10. });
    
9. 删除指定的日历账户，删除账户后，该账户下的所有日程会全部删除。
    
    1. // Index.ets
    2. calendarMgr?.deleteCalendar(calendar).then(() => {
    3.  console.info("Succeeded in deleting calendar");
    4. }).catch((err: BusinessError) => {
    5.  console.error(`Failed to delete calendar. Code: ${err.code}, message: ${err.message}`);
    6. });
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/calendarmanager-overview "Calendar Kit简介")
# 日程管理

更新时间: 2025-12-16 16:36

日程指特定的事件或者活动安排，日程管理即对这些事件、活动进行规划和控制，能更有效地利用相关资源、提高生产力和效率，使人们更好地管理时间和任务。

Calendar Kit中的日程[Event](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-calendarmanager#event)归属于某个对应的日历账户[Calendar](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-calendarmanager#calendar)，一个日历账户下可以有多个日程，一个日程只属于一个Calendar。

获取到日历账户对象之后，即可对该账户下的日程进行管理，包括日程的创建、删除、修改、查询等操作。在创建、修改日程时，支持对日程的标题、开始时间、结束时间、日程类型、日程地点、日程提醒时间、日程重复规则等相关信息进行设置，以便进行更丰富更有效的日程管理。

## 接口说明

以下是日程管理的相关接口，更多详细接口及使用请参考[@ohos.calendarManager](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-calendarmanager)。

|接口名称|描述|
|:--|:--|
|getCalendarManager(context: Context): CalendarManager|根据上下文获取CalendarManager对象，用于管理日历。|
|createCalendar(calendarAccount: CalendarAccount): Promise<Calendar>|根据日历账户信息，创建一个Calendar对象，使用Promise异步回调。|
|addEvent(event: Event): Promise<number>|创建日程，入参Event不填日程id，使用Promise异步回调。|
|editEvent(event: Event): Promise<number>|通过跳转到日程创建界面创建单个日程，入参Event不填日程id，使用Promise异步回调。|
|deleteEvent(id: number): Promise<void>|删除指定日程id的日程，使用Promise异步回调。|
|updateEvent(event: Event): Promise<void>|更新日程，使用Promise异步回调。|
|getEvents(eventFilter?: EventFilter, eventKey?: (keyof Event)[]): Promise<Event[]>|获取Calendar下符合查询条件的Event，使用Promise异步回调。|

## 开发步骤

1. 导入相关依赖。
    
    1. // entry/src/main/ets/entryability/EntryAbility.ets
    2. import { abilityAccessCtrl, AbilityConstant, common, PermissionRequestResult, Permissions, UIAbility, Want } from '@kit.AbilityKit';
    3. import { BusinessError } from '@kit.BasicServicesKit';
    4. import { calendarManager } from '@kit.CalendarKit';
    5. import { window } from '@kit.ArkUI';
    
2. 申请权限。使用Calendar Kit时，需要在module.json5中声明申请读写日历日程所需的权限：ohos.permission.READ_CALENDAR和ohos.permission.WRITE_CALENDAR。具体指导可见[声明权限](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/declare-permissions)。
    
3. 根据上下文获取日程管理器对象calendarMgr，用于对日历账户进行相关管理操作。推荐在EntryAbility.ets文件中进行操作。
    
    1. // entry/src/main/ets/entryability/EntryAbility.ets
    2. export let calendarMgr: calendarManager.CalendarManager | null = null;
    
    3. export let mContext: common.UIAbilityContext | null = null;
    
    4. export default class EntryAbility extends UIAbility {
    5.   onCreate(want: Want, launchParam: AbilityConstant.LaunchParam): void {
    6.     console.info("Ability onCreate");
    7.   }
    
    8.   onDestroy(): void {
    9.     console.info("Ability onDestroy");
    10.   }
    
    11.   onWindowStageCreate(windowStage: window.WindowStage): void {
    12.     // Main window is created, set main page for this ability
    13.     console.info("Ability onWindowStageCreate");
    14.     windowStage.loadContent('pages/Index', (err, data) => {
    15.       if (err.code) {
    16.         console.error(`Failed to load the content. Code: ${err.code}, message: ${err.message}`);
    17.         return;
    18.       }
    19.       console.info(`Succeeded in loading the content. Data: ${JSON.stringify(data)}`);
    20.     });
    21.     mContext = this.context;
    22.     const permissions: Permissions[] = ['ohos.permission.READ_CALENDAR', 'ohos.permission.WRITE_CALENDAR'];
    23.     let atManager = abilityAccessCtrl.createAtManager();
    24.     atManager.requestPermissionsFromUser(mContext, permissions).then((result: PermissionRequestResult) => {
    25.       console.info(`get Permission success, result: ${JSON.stringify(result)}`);
    26.       calendarMgr = calendarManager.getCalendarManager(mContext);
    27.     }).catch((error: BusinessError) => {
    28.       console.error(`get Permission error, error. Code: ${error.code}, message: ${error.message}`);
    29.     })
    30.   }
    
    31.   onWindowStageDestroy(): void {
    32.     // Main window is destroyed, release UI related resources
    33.     console.info("Ability onWindowStageDestroy");
    34.   }
    
    35.   onForeground(): void {
    36.     // Ability has brought to foreground
    37.     console.info("Ability onForeground");
    38.   }
    
    39.   onBackground(): void {
    40.     // Ability has back to background
    41.     console.info("Ability onBackground");
    42.   }
    43. }
    
4. 根据日历账户信息创建Calendar对象，用于进行日程管理。设置日历配置信息，可以根据需要打开日程提醒、设置日历账户颜色。
    
    1. // Index.ets
    2. import { BusinessError } from '@kit.BasicServicesKit';
    3. import { calendarMgr } from '../entryability/EntryAbility';
    4. import { calendarManager } from '@kit.CalendarKit';
    
    5. let calendar: calendarManager.Calendar | undefined = undefined;
    6. // 指定日历账户信息
    7. const calendarAccount: calendarManager.CalendarAccount = {
    8.   name: 'MyCalendar',
    9.   type: calendarManager.CalendarType.LOCAL,
    10.   // 日历账户显示名称，该字段如果不填，创建的日历账户在界面显示为空字符串。
    11.   displayName: 'MyCalendar'
    12. };
    13. // 日历配置信息
    14. const config: calendarManager.CalendarConfig = {
    15.   // 打开日程提醒
    16.   enableReminder: true,
    17.   // 设置日历账户颜色
    18.   color: '#aabbcc'
    19. };
    20. // 创建日历账户
    21. calendarMgr?.createCalendar(calendarAccount).then((data: calendarManager.Calendar) => {
    22.   console.info(`Succeeded in creating calendar data->${JSON.stringify(data)}`);
    23.   calendar = data;
    24.   // 请确保日历账户创建成功后，再进行相关日程的管理
    
    25.   // 设置日历配置信息，打开日程提醒、设置日历账户颜色
    26.   calendar.setConfig(config).then(() => {
    27.     console.info(`Succeeded in setting config, data->${JSON.stringify(config)}`);
    28.   }).catch((err: BusinessError) => {
    29.     console.error(`Failed to set config. Code: ${err.code}, message: ${err.message}`);
    30.   });
    31.   // ...
    32. }).catch((error: BusinessError) => {
    33.   console.error(`Failed to create calendar. Code: ${error.code}, message: ${error.message}`);
    34. });
    
5. 在当前日历账户下添加日历日程，注意入参中不需要填写日程id。
    
    创建日程时，支持设置日程的标题、开始时间、结束时间、日程类型、日程地点、日程提醒时间、日程重复规则等相关信息。
    
    日程创建成功后会返回一个日程id，作为日程的唯一标识，后续可按照日程id进行指定日程的更新或删除。
    
    目前支持以下两种方式来创建日程。
    
    方式一：可以在日历账户下通过addEvent()或addEvents()接口创建日程。其中可使用addEvent()接口创建单个日程，也可以使用addEvents()接口批量创建日程，此处以创建单个日程为例。
    
    方式二：在获取到日历管理器对象后，可通过editEvent()接口创建单个日程。调用此接口创建日程时，会跳转到日程创建页面，在日程创建页面进行相关操作完成日程的创建, editEvent()不支持自定义周期性日程创建。
    
    1. // Index.ets
    2. let eventId : number | undefined = undefined;
    3. const date = new Date();
    4. const event: calendarManager.Event = {
    5.   // 日程标题
    6.   title: 'title',
    7.   // 日程类型，不推荐三方开发者使用calendarManager.EventType.IMPORTANT，重要日程类型不支持一键服务跳转功能及无法自定义提醒时间
    8.   type: calendarManager.EventType.NORMAL,
    9.   // 日程开始时间
    10.   startTime: date.getTime(),
    11.   // 日程结束时间
    12.   endTime: date.getTime() + 60 * 60 * 1000,
    13.   // 距开始时间提前10分钟提醒
    14.   reminderTime: [10],
    15.   // 日程重复规则，可选属性。如果日程为周期性日程需要填写该属性。
    16.   recurrenceRule: {
    17.     // 日程重复规则类型，支持按天、按周、按月、按年重复
    18.     recurrenceFrequency: calendarManager.RecurrenceFrequency.DAILY,
    19.     // 日程重复次数，该字段和expire属性只需要填写一个，如果两个都填写按照count属性计算。
    20.     count: 100,
    21.     // 重复日程间隔时间，与recurrenceFrequency相关，此示例表示日程每隔2天进行重复。
    22.     interval: 2,
    23.     // 日程过期时间，该字段和count属性只需要填写一个，如果两个都填写按照count属性计算。
    24.     expire: date.getTime() + 60 * 60 * 1000 * 3,
    25.     // 日程排除日期，将该日期从重复日程中排除掉
    26.     excludedDates: [date.getTime() + 60 * 60 * 1000 * 2]
    27.   },
    28.   // 日程服务，可选字段，需要一键服务功能的日程，填写该属性。
    29.   service: {
    30.     // 服务类型，比如一键查看、一键入会、一键追剧等。
    31.     type: calendarManager.ServiceType.TRIP,
    32.     // 服务的uri。可以跳转到三方应用相应界面，格式为DeepLink。使用DeepLink方式需要在华为HAG云侧进行注册，注册提供的信息为应用包名、应用的服务类型。
    33.     // DeepLink包括scheme、host、path以及参数（不包含参数值）
    34.     uri: 'xxx://xxx.xxx.com/xxx',
    35.     // 服务辅助描述信息，可选字段
    36.     description: '一键服务'
    37.   }
    
    38. };
    39. // 方式一
    40. calendar.addEvent(event).then((data: number) => {
    41.   console.info(`Succeeded in adding event, id -> ${data}`);
    42.   eventId = data;
    43. }).catch((err: BusinessError) => {
    44.   console.error(`Failed to addEvent. Code: ${err.code}, message: ${err.message}`);
    45. });
    46. // 方式二
    47. const eventInfo: calendarManager.Event = {
    48.   // 日程标题
    49.   title: 'title',
    50.   // 日程类型
    51.   type: calendarManager.EventType.NORMAL,
    52.   // 日程开始时间
    53.   startTime: date.getTime(),
    54.   // 日程结束时间
    55.   endTime: date.getTime() + 60 * 60 * 1000
    56. };
    57. calendarMgr?.editEvent(eventInfo).then((id: number): void => {
    58.   console.info(`create Event id = ${id}`);
    59.   eventId = id;
    60. }).catch((err: BusinessError) => {
    61.   console.error(`Failed to create Event. Code: ${err.code}, message: ${err.message}`);
    62. });
    
6. 按照日程id进行指定日程的更新，更新日程相关信息。
    
    1. // Index.ets
    2. const updateEvent: calendarManager.Event = {
    3.   title: 'updateTitle',
    4.   description: 'updateEventTest',
    5.   type: calendarManager.EventType.NORMAL,
    6.   id: eventId,
    7.   startTime: date.getTime(),
    8.   endTime: date.getTime() + 60 * 60 * 1000
    9. };
    10. calendar.updateEvent(updateEvent).then(() => {
    11.   console.info(`Succeeded in updating event`);
    12. }).catch((err: BusinessError) => {
    13.   console.error(`Failed to update event. Code: ${err.code}, message: ${err.message}`);
    14. });
    
7. 查询当前日历账户下的所有日程。由于涉及数据隐私安全，进行了权限管控的应用无法获取其他创建的日程信息。根据不同的查询条件和查询字段，返回不同的查询结果。
    
    当没有查询条件和查询字段时，可查询指定日历账户下的所有日程。
    
    1. calendar.getEvents().then((data: calendarManager.Event[]) => {
    2.   console.info(`Succeeded in getting events, data -> ${JSON.stringify(data)}`);
    3. }).catch((err: BusinessError) => {
    4.   console.error(`Failed to get events. Code: ${err.code}, message: ${err.message}`);
    5. });
    
    还支持根据日程id、日程开始和结束时间、日程标题等查询条件来查询日程。
    
    6. // 根据日程id查询
    7. const filterId = calendarManager.EventFilter.filterById([eventId]);
    8. calendar.getEvents(filterId).then((data: calendarManager.Event[]) => {
    9.   console.info(`Succeeded in getting events, data -> ${JSON.stringify(data)}`);
    10. }).catch((err: BusinessError) => {
    11.   console.error(`Failed to get events. Code: ${err.code}, message: ${err.message}`);
    12. });
    
    13. // 根据日程标题查询
    14. const filterTitle = calendarManager.EventFilter.filterByTitle('update');
    15. calendar.getEvents(filterTitle).then((data: calendarManager.Event[]) => {
    16.   console.info(`Succeeded in getting events, data -> ${JSON.stringify(data)}`);
    17. }).catch((err: BusinessError) => {
    18.   console.error(`Failed to get events. Code: ${err.code}, message: ${err.message}`);
    19. });
    
    20. // 根据日程开始和结束时间查询
    21. const filterTime = calendarManager.EventFilter.filterByTime(1686931200000, 1687017600000);
    22. calendar.getEvents(filterTime).then((data: calendarManager.Event[]) => {
    23.   console.info(`Succeeded in getting events filter by time, data -> ${JSON.stringify(data)}`);
    24. }).catch((err: BusinessError) => {
    25.   console.error(`Failed to filter by time. Code: ${err.code}, message: ${err.message}`);
    26. });
    
8. 按照日程id进行指定日程的删除。可以通过deleteEvent()接口进行单个日程的删除，也可以通过deleteEvents()接口批量删除指定日程，此处以删除单个指定日程为例。
    
    1. // Index.ets
    2. calendar.deleteEvent(eventId).then(() => {
    3.    console.info("Succeeded in deleting event");
    4.  }).catch((err: BusinessError) => {
    5.    console.error(`Failed to delete event. Code: ${err.code}, message: ${err.message}`);
    6. });
    

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/calendarmanager-calendar-developer "日历账户管理")
# 注册并管理一键服务日程

更新时间: 2025-12-16 16:36

## 场景介绍

Calendar Kit提供日程一键服务功能，比如一键入会、一键追剧、一键购物、一键查看等。注册日程一键服务后，用户可通过点击对应按钮拉起跳转链接，一步直达服务落地页，方便快捷。

## 服务器注册（白名单配置）

若需使用“日程一键服务”功能，需要按照以下步骤完成注册。

1. 进入[开发者管理中心](https://developer.huawei.com/consumer/cn/console/overview)，登录[企业账号](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/store-attribution-config-agc)（暂不支持个人开发者）。企业主账号无需手动添加权限；若使用团队成员账号，请确保使用企业主账号为其添加“小艺开放平台”的管理员权限，具体添加可见下图。
    
    选择团队账号，点击编辑，为对应的账号添加权限。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163615.34627699701715087109264833713406:50001231000000:2800:EA1DE3A3E5F8C12377B87A7E7E565045372776644C00826F3BC83A8FCE269557.png "点击放大")
    
    确认对应的信息后，点击下一步。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163615.99572343805746382227568465920171:50001231000000:2800:D70FF800886093E49141D66D7D1E08CA1E4AB384E0823729A458DC387B7E74B7.png "点击放大")
    
    勾选小艺开放平台管理员，选择下一步。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163615.55231807800235801662531777091326:50001231000000:2800:B67AE7D61086CAE6D6F6DDA18F74C7E49A00644B6DAA8DEECD01CCB0EAD60D50.png "点击放大")
    
2. 登录成功后，在侧边栏菜单中**生态服务**下选择**智慧服务**，点击进入**小艺开放平台**。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163615.41646821935135670084548316474898:50001231000000:2800:A04B75C7FB2CB5628AB5A4DD0FA2DD87418117EC354D84FC2DA106471E5F86A3.png "点击放大")
    
3. 进入页面后，选择右侧**资源管理**，点击选择**其他服务**。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163615.94386920904484689298207914220011:50001231000000:2800:B64764EC4222F49A83F92B055B0CF3DC08E9F14EDE807A4949E2D98B186B71E5.png "点击放大")
    
4. 进入页面后，点击右侧**创建服务**按钮。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163615.77889575669443174502641087444214:50001231000000:2800:DCB44AB5162445BCAA7DFFB10B7FBAC0D8E9C6C45B7607235C9E4AC2F9370029.png "点击放大")
    
5. 选择服务模型。
    
    选择**自定义模型**，填写**服务名称**、**服务分类**、**默认语言**，点击**创建**按钮。
    
    **服务名称**：可由用户自定义，推荐使用“应用名+日历一键服务”的组合命名形式。
    
    **服务分类**：开发者根据实际业务类型自行选择。
    
    **默认语言**：由开发者根据业务选择配置。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163615.30229490342716530566163110948646:50001231000000:2800:52D0605905E6E6B38F5CA858F16C97A088713402609F001C0C55F287FB72CDF6.png "点击放大")
    
6. 创建完成后，填写服务的**基本信息**，点击**保存**按钮。
    
    **服务分类**：选择实用工具/日历。
    
    **服务版本号**和**版本描述**可由开发者自定义，平台审核不关注此信息。
    
    **服务分级**：由开发者根据业务选择配置。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163615.68094508657653838283050987014857:50001231000000:2800:499D16349A1829A11C3C17226366A1792E0753D70823C70A8D9FF75B99C99108.png "点击放大")
    
7. 填写**服务呈现****信息**，点击**保存**按钮。
    
    此页面必填字段均由开发者根据业务选择配置。建议在服务预览处上传用户界面示意图。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163615.74390587392360452718768392858348:50001231000000:2800:D3DFF6F1C533B827C1AAC1BC94886E3FAEC78FFBBAF506243DB4CEDA01232BC0.png "点击放大")
    
8. 进入**配置**，选择**新增用户意图**。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163615.26740242637453392837809688545571:50001231000000:2800:DB7FAFB45783B3F46BC661C0EC6E0912669A08F99E684263837650C69D1E3045.png "点击放大")
    
9. 配置意图。
    
    1. 设置**意图标识**、**意图名称**和**意图分类**，勾选一键服务。意图分类选择“查日历”。
    2. 勾选一键服务之后，选择**服务类型**（请与Calendar Kit提供的日程服务类型[ServiceType](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-calendarmanager#servicetype)一致），点击**添加关联**按钮，输入**app包名**及**app名称**（请确保app包名及app名称准确匹配，否则一键服务无法生效）。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163616.25685317312325087899169360600829:50001231000000:2800:4914D56A838E542D78736404CC852283F7B454C3EF350891D12F305617A76372.png "点击放大")
    
10. 配置意图的**实现类型**，选择**APK/RPK/FA/H5 link**，选择**新增实现**，点击**配置**按钮。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163616.04334309414631129178939221550835:50001231000000:2800:F559D3BCF52B9B128CB375FFEF8DACA35C258E6415D3E7D42F2970AF155CF5D0.png "点击放大")
    
11. 进入新增实现页面，填写**基本信息**和**配置方式**后，选择**保存**。
    
    1. 填写基本信息。实现名称由开发者根据业务自定义，推荐使用“应用名+一键服务类型”命名。
    2. 选择配置方式，勾选**HAP LINK**。
        
        填写准确的**App名称**（若下拉菜单中无匹配项，可直接输入）和**A****pp包名**。
        
        填写**跳转链接**，即用户在系统日历中点击一键服务按钮拉起的落地页；请勿打开**跳转参数**开关。
        
        说明
        
        跳转链接为链接模板，实际[EventService](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-calendarmanager#eventservice)填入的uri需遵循此模板。例如，若填写跳转链接为“**demo****://mobile/player?****params=**”，则对应可匹配的uri为“**demo****://mobile/player****?****params****=**AAAABBBBCCCCDDDD”，其中加粗部分为强校验，未加粗部分可由业务方根据需要自定义。
        
        其他必填字段，由开发者根据业务自行配置。
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163616.03651346561520293312590835738582:50001231000000:2800:452D5BD166B53C112B69705F66E08FE2E5F6FE1DE77B1B7C359A846CDF633F14.png "点击放大")
        
        ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163616.57124895501456667618505958050518:50001231000000:2800:6051227D491ED076EB2683F106DC7FE38EAFBD557A072FB38CB582ABFB69B9BA.png "点击放大")
        
    
12. 完成以上所有配置后，切换到**发布**模块，点击**上架**按钮，等待后台审核后，完成意图发布。
    
    说明
    
    若已完成上架的服务，支持根据上文步骤再次调整修改，修改完成后，点击**升级**。
    
    ![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163616.57633348099911873176089108516120:50001231000000:2800:2281B4F26A5E80579C0B383AA27EEBBB396372383DA891DA9C3124A89042F329.png "点击放大")
    

## 客户端添加一键服务日程

一键服务注册成功后，即完成系统日历跳转白名单配置（支持在系统日历界面显示对应功能按钮）；若想实现一键服务体验，还需在客户端进行相关配置。

配置步骤如下：

1. 在module.json5文件中，配置相关字段。
    
    需配置"exported"字段为true。
    
    并配置["skills"](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/module-configuration-file#skills%E6%A0%87%E7%AD%BE)中的"actions"字段，"actions"标识能够接收的Action值集合，取值通常为系统预定义的action值，也允许自定义。actions不能为空，actions为空会造成目标方匹配失败，常见的action取值可见[action常数说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-ability-wantconstant#action)。
    
    最后配置"uris"字段，"uris"需与注册时的链接模板相匹配。
    
    比如，服务器端注册时填写的uri模板链接若为"demo://mobile/player?params="，则“=”前的内容为强校验，“=”后的内容为**业务需要使用的参数列表**，可在使用日历服务写入日程时根据各业务实际情况进行指定。参数列表中不得直接包含字符“=”或“&”，请注意使用decodeURI()/encodeURI()进行转换。
    
    1. {
    2.   "module": {
    3.     "name": "xxx",
    4.     "type": "xxx",
    5.     // ...
    6.     "abilities": [
    7.       {
    8.         "name": "xxxxxxx",
    9.         // ...
    10.         "exported": true,
    11.         "skills": [
    12.           {
    13.             // ...
    14.            "actions": [
    15.              "ohos.want.action.viewData"
    16.             ],
    17.             "uris": [
    18.               {
    19.                 "scheme":"demo",
    20.                 "host":"mobile",
    21.                 "pathStartWith": "player"
    22.               }
    23.             ],
    24.           }
    25.         ]
    26.       }
    27.     ],
    28.   }
    29. }
    
2. 在被拉起的落地页EntryAbility中的onCreate、onNewWant接口中的want对象内存在对应的拉起信息，开发者可通过对应参数实现对应跳转逻辑，本文不再赘述。
3. 调用[addEvent](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-calendarmanager#addevent)接口添加日程数据，后续即可见日历内出现含一键服务按钮的日程，点击即可跳转至对应落地页。

## 约束限制

- 普通日程（EventType.NORMAL）可以提供一键服务按钮的露出；重要日程（EventType.IMPORTANT）因数据结构和产品规格限制，即使配置正确也无法提供一键服务。
- 该服务仅在用户设备联网下载对应协议后，开发者写入的日程才会显示对应按钮。
- 一键服务按钮的展示规则为：日程详情内始终展示，月视图、桌面卡片在日程开始前15分钟展示。
- 在服务器端注册的服务协议完成上架，审核通过后，设备恢复出厂设置，或待当天零点后，功能可正式生效。
- 请确保服务器端填写的链接模版（[服务器注册（白名单配置）](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/calendar-service#section105171945105213)）、设备端三方应用侧写入的Event.Service.uri、module.json5配置的"uris"字段信息（[客户端添加一键服务日程](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/calendar-service#section104061249387)）相互匹配。

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/calendarmanager-event-developer "日程管理")# 日历服务实践案例

更新时间: 2025-12-16 16:36

## 场景介绍

通过日历服务，开发者可将带有时间属性的事件作为日程写入，并支持通过“[一键服务](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/calendar-service)”功能快速跳转，帮助用户快速直达对应服务，并完成各类信息的归一化管理。各典型场景选择适用的模板，并按照模板格式填写各个字段信息，确保用户体验完整、一致。

写入日历的日程可通过通知中心、桌面卡片以及日历应用内部等多种入口向用户展示。

不同场景下，一键服务按钮出现时机如下：

- 桌面卡片、月视图日程列表卡片：日程开始时间前15分钟显示，日程结束时自动隐藏。
- 日程详情：始终显示。
- 日程通知：通知弹出时显示，通知中心内点击对应日程卡片后显示。

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163618.32294140748008304658538323225995:50001231000000:2800:96599B6A50501E21F40CD01404D5C8D429BDDB594B9F653519BC685614676194.png "点击放大")

## 开发准备

请参考日程管理前三步的[开发步骤](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/calendarmanager-calendar-developer#%E5%BC%80%E5%8F%91%E6%AD%A5%E9%AA%A4)：

1. 导入相关依赖。
    
2. 申请权限。使用Calendar Kit时，需要在module.json5中声明申请读写日历日程所需的权限：ohos.permission.READ_CALENDAR和ohos.permission.WRITE_CALENDAR。具体指导可见[声明权限](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/declare-permissions)。
    
3. 根据上下文获取日程管理器对象calendarMgr，用于对日历账户进行相关管理操作。推荐在EntryAbility.ets文件中进行操作。
    

## 一键服务典型场景

一键服务典型场景及对应显示内容如下表所示：

|场景类型|[ServiceType取值](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-calendarmanager#servicetype)|按钮显示内容|
|:--|:--|:--|
|会议|'Meeting'|加入会议|
|追剧|'Watching'|立即观看|
|还款|'Repayment'|马上还款|
|直播|'Live'|开启直播|
|购物|'Shopping'|开始选购|
|查看|'Trip'|立即查看|
|上课|'Class'|开始上课|
|赛事|'SportsEvents'|立即观看|
|运动|'SportsExercise'|开始运动|

在进行各场景的开发前，请确保已导入相关依赖、申请相关权限等，具体可见[开发准备](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/calendarmanager-practice-developer#%E5%BC%80%E5%8F%91%E6%AD%A5%E9%AA%A4)。

### 出行服务场景

当用户通过购票平台预订火车票、机票或其他交通方式后，系统可以自动将其行程信息添加至日历，并在适当的时间节点进行提醒。

下表列出了该场景中主要字段的推荐配置及其说明：

|字段名称|对应设置项|建议取值|
|:--|:--|:--|
|日程标题|title|航班、车次信息加出发地、目的地信息|
|开始时间|startTime|行程开始时间|
|结束时间|endTime|行程结束时间|
|提醒时间|reminderTime|2小时前、4小时前分别提醒|
|日历账户（在日历中对用户体现）|displayName|生态应用名（建议与应用市场中名称一致）|
|备注|description|可补充检票口信息、座位号信息|
|一键服务|ServiceType|calendarManager.ServiceType.TRIP|

1. 创建日程。
    
    1. // Index.ets
    2. import { calendarMgr } from '../entryability/EntryAbility';
    3. import { calendarManager } from '@kit.CalendarKit';
    
    4. let tripCalendar: calendarManager.Calendar | undefined = undefined;
    5. let oriEvent: calendarManager.Event | null = null;
    6. let id: number = 0;
    
    7. async createTripCalendarAndEvent(): Promise<void> {
    8.   // 指定日历账户信息
    9.   const calendarAccount: calendarManager.CalendarAccount = {
    10.     name: 'TripCalendar',
    11.     type: calendarManager.CalendarType.LOCAL,
    12.     // 日历账户显示名称：建议使用应用实际名称。
    13.     displayName: '高铁出行'
    14.   };
    15.   // 日历配置信息
    16.   const config: calendarManager.CalendarConfig = {
    17.     // 设置日历账户颜色
    18.     color: '#aabbcc'
    19.   };
    20.   const startTime = new Date('2025-10-01T08:17:00').getTime();
    21.   const endTime = new Date('2025-10-01T12:51:00').getTime();
    22.   // 日程配置信息
    23.   const event: calendarManager.Event = {
    24.     type: calendarManager.EventType.NORMAL,
    25.     // 日程标题
    26.     title: '行程信息：G107 上海虹桥-北京南',
    27.     // 开始时间
    28.     startTime: startTime,
    29.     // 结束时间
    30.     endTime: endTime,
    31.     // 是否全天日程
    32.     isAllDay:false,
    33.     // 提醒时间
    34.     reminderTime:[120, 240],
    35.     // 备注
    36.     description: '检票口：南二楼1口或北广场B2候车室 \n座位号：02车04二等座',
    37.     // 一键服务
    38.     service: {
    39.       // 服务类型
    40.       type: calendarManager.ServiceType.TRIP,
    41.       // 服务的uri，格式为DeepLink类型。请根据“[一键服务](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/calendar-service)”指导文档配置。
    42.       uri: 'demo://mobile/player?params='
    43.     }
    44.   }
    45.   try {
    46.     // 创建日历账户
    47.     tripCalendar = await calendarMgr?.createCalendar(calendarAccount);
    48.     if (!tripCalendar || tripCalendar === null) {
    49.       console.error('Failed to create calendar. tripCalendar is null.');
    50.       return;
    51.     }
    52.     // 请确保日历账户创建成功后，再进行相关日程的管理
    53.     // 设置日历配置信息，设置日历账户颜色
    54.     await tripCalendar.setConfig(config);
    55.     // 添加日程
    56.     id = await tripCalendar.addEvent(event);
    57.     oriEvent = event;
    58.     oriEvent.id = id;
    59.     console.info(`Succeeded in creating calendar and event, result: ${JSON.stringify(id)}`);
    60.   } catch (error) {
    61.     console.error(`Failed to create calendar or event. Code: ${error.code}, message: ${error.message}`);
    62.   }
    63. }
    
2. 查询日程。
    
    1. // Index.ets
    2. async getTripEvent(): Promise<void> {
    3.   // 校验calendar是否为空
    4.   if (!tripCalendar || tripCalendar === null) {
    5.     console.error('Failed to get event, calendar is null.');
    6.     return;
    7.   }
    8.   try {
    9.     // 查询行程
    10.     const filter = calendarManager.EventFilter.filterById([id]);
    11.     let data: calendarManager.Event[] = await tripCalendar.getEvents(filter, ['title', 'type', 'startTime', 'endTime']);
    12.     if (data && data.length > 0) {
    13.       oriEvent = data[0];
    14.     }
    15.     console.info(`Succeeded in getting events, data -> ${JSON.stringify(data)}`);
    16.   } catch (err) {
    17.     console.error(`Failed to get events. Code: ${err.code}, message: ${err.message}`);
    18.   }
    19. }
    
3. 更新日程。
    
    1. // Index.ets
    2. async updateTripEvent(): Promise<void> {
    3.   // 校验calendar是否为空
    4.   if (!tripCalendar || tripCalendar === null) {
    5.     console.error('Failed to update event, calendar is null.');
    6.     return;
    7.   }
    8.   if (!oriEvent || oriEvent === null) {
    9.     console.error('Failed to update event, oriEvent is null');
    10.     return;
    11.   }
    12.   // 修改行程的开始时间startTime和结束时间endTime
    13.   oriEvent.startTime = new Date('2025-10-01T07:03:00').getTime();
    14.   oriEvent.endTime = new Date('2025-10-01T11:51:00').getTime();
    15.   try {
    16.     // 更新行程
    17.     await tripCalendar.updateEvent(oriEvent);
    18.     console.info("Succeeded in updating event");
    19.   } catch (err) {
    20.     console.error(`Failed to update event. Code: ${err.code}, message: ${err.message}`);
    21.   }
    22. }
    
4. 删除日程。
    
    1. // Index.ets
    2. async deleteTripEvent(): Promise<void> {
    3.   // 校验calendar是否为空
    4.   if (!tripCalendar || tripCalendar === null) {
    5.     console.error('Failed to delete event, calendar is null.');
    6.     return;
    7.   }
    8.   try {
    9.     // 删除行程
    10.     await tripCalendar.deleteEvent(id);
    11.     oriEvent = null;
    12.     console.info(`Succeeded in deleting Event`);
    13.   } catch (err) {
    14.     console.error(`Failed to delete Event, Code is ${err.code}, message is ${err.message}`);
    15.   }
    16. }
    

示意图如下：

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163618.32171668430338963414422331906506:50001231000000:2800:C4983131681A226978CC4853F44FEC4B0E39D18CB99459369176D7F5798C4C4A.png)

### 酒店住宿场景

下表列出了该场景中主要字段的推荐配置及其说明：

|字段名称|对应设置项|建议取值|
|:--|:--|:--|
|日程标题|title|酒店入住信息（酒店标题地址）|
|地点|[location](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-calendarmanager#location)|酒店的地理位置|
|开始时间|startTime|入住时间|
|结束时间|endTime|离店时间|
|全天日程|isAllDay|true：表示添加全天日程。|
|提醒时间|reminderTime|0：全天日程时表示当天上午9点提醒（非全天日程则是日程开始时间）。<br><br>1440：表示前一天上午9点提醒。<br><br>不填时，默认为不提醒。|
|日历账户（在日历中对用户体现）|displayName|生态应用名（建议与应用市场中名称一致）|
|备注|description|可补充入住时间、离店时间信息|
|一键服务|ServiceType|calendarManager.ServiceType.Trip|

创建日程示例和示意图如下：

1. // Index.ets
2. async createHotelCalendarAndEvent(): Promise<void> {
3.   // 指定日历账户信息
4.   const calendarAccount: calendarManager.CalendarAccount = {
5.     name: 'hotelCalendar',
6.     type: calendarManager.CalendarType.LOCAL,
7.     // 日历账户显示名称：建议使用应用实际名称。
8.     displayName: '酒店住宿'
9.   };
10.   // 日历配置信息
11.   const config: calendarManager.CalendarConfig = {
12.     // 设置日历账户颜色
13.     color: '#aabbcc'
14.   };
15.   const startTime = new Date('2025-05-01T15:00:00').getTime();
16.   const endTime = new Date('2025-05-02T12:00:00').getTime();
17.   // 日程配置信息
18.   const event: calendarManager.Event = {
19.     type: calendarManager.EventType.NORMAL,
20.     title: '入住信息:酒店(上海新天地店)',
21.     location: {
22.       location: '上海新天地',
23.       longitude: 121.47506199999998,
24.       latitude: 31.219150000000013
25.     },
26.     startTime: startTime,
27.     endTime: endTime,
28.     isAllDay: true,
29.     // 提醒时间：全天日程是按9点往前计算分钟数
30.     reminderTime: [0, 1440],
31.     description: '入住:15:00后\n离店:12:00前',
32.     // 一键服务
33.     service: {
34.       type: calendarManager.ServiceType.TRIP,
35.       uri: 'demo://mobile/player?params='
36.     }
37.   }
38.   try {
39.     // 创建日历账户
40.     let data: calendarManager.Calendar | undefined= await calendarMgr?.createCalendar(calendarAccount);
41.     if (!data || data === null) {
42.       console.error('Failed to create calendar. data is null.');
43.       return;
44.     }
45.     // 请确保日历账户创建成功后，再进行相关日程的管理
46.     // 设置日历配置信息，设置日历账户颜色
47.     await data.setConfig(config);
48.     // 添加日程
49.     id = await data.addEvent(event);
50.     console.info(`Succeeded in creating calendar and event, result: ${JSON.stringify(id)}`);
51.   } catch (error) {
52.     console.error(`Failed to create calendar or event. Code: ${error.code}, message: ${error.message}`);
53.   }
54. }

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163618.31624232948300589986181712884728:50001231000000:2800:E52709D0441294D7AB1ED0FE142843C713855E26AED029A185306B1C8870A91A.png "点击放大")

### 直播预约场景

下表列出了该场景中主要字段的推荐配置及其说明：

|字段名称|对应设置项|建议取值|
|:--|:--|:--|
|日程标题|title|直播名称|
|开始时间|startTime|直播开始时间|
|结束时间|endTime|直播结束时间|
|提醒时间|reminderTime|准时、10分钟前分别提醒|
|日历账户（在日历中对用户体现）|displayName|生态应用名（建议与应用市场中名称一致）|
|备注|description|可补充直播相关详情介绍|
|一键服务|ServiceType|calendarManager.ServiceType.Live|

创建日程示例和示意图如下：

1. // Index.ets
2. async createLiveCalendarAndEvent(): Promise<void> {
3.   // 指定日历账户信息
4.   const calendarAccount: calendarManager.CalendarAccount = {
5.     name: 'liveCalendar',
6.     type: calendarManager.CalendarType.LOCAL,
7.     // 日历账户显示名称：建议使用应用实际名称。
8.     displayName: '直播抢购'
9.   };
10.   // 日历配置信息
11.   const config: calendarManager.CalendarConfig = {
12.     // 设置日历账户颜色
13.     color: '#aabbcc'
14.   };
15.   const startTime = new Date('2025-11-04T21:00:00').getTime();
16.   const endTime = new Date('2025-11-04T22:00:00').getTime();
17.   // 日程配置信息
18.   const event: calendarManager.Event = {
19.     type: calendarManager.EventType.NORMAL,
20.     title: '直播抢购',
21.     startTime: startTime,
22.     endTime: endTime,
23.     isAllDay: false,
24.     reminderTime: [0, 10],
25.     description: '限时特惠,秋季最大福利就在直播间',
26.     // 一键服务
27.     service: {
28.       type: calendarManager.ServiceType.LIVE,
29.       uri: 'demo://mobile/player?params='
30.     }
31.   }
32.   try {
33.     // 创建日历账户
34.     let data: calendarManager.Calendar | undefined= await calendarMgr?.createCalendar(calendarAccount);
35.     if (!data || data === null) {
36.       console.error('Failed to create calendar. data is null.');
37.       return;
38.     }
39.     // 请确保日历账户创建成功后，再进行相关日程的管理
40.     // 设置日历配置信息，设置日历账户颜色
41.     await data.setConfig(config);
42.     // 添加日程
43.     id = await data.addEvent(event);
44.     console.info(`Succeeded in creating calendar and event, result: ${JSON.stringify(id)}`);
45.   } catch (error) {
46.     console.error(`Failed to create calendar or event. Code: ${error.code}, message: ${error.message}`);
47.   }
48. }

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163618.07872570076054225494950043475403:50001231000000:2800:610579A05756A4E0BEF7373173459540C5AD0BC35167A001B067A830D5A9B2EE.png)

### 抢购预约场景

下表列出了该场景中主要字段的推荐配置及其说明：

|字段名称|对应设置项|建议取值|
|:--|:--|:--|
|日程标题|title|购物节（抢购活动）名称|
|开始时间|startTime|抢购开始时间|
|结束时间|endTime|抢购结束时间|
|提醒时间|reminderTime|准时、10分钟前分别提醒|
|日历账户（在日历中对用户体现）|displayName|生态应用名（建议与应用市场中名称一致）|
|备注|description|可补充购物节相关介绍|
|一键服务|ServiceType|calendarManager.ServiceType.Shopping|

创建日程示例和示意图如下：

1. // Index.ets
2. async createShoppingCalendarAndEvent(): Promise<void> {
3.   // 指定日历账户信息
4.   const calendarAccount: calendarManager.CalendarAccount = {
5.     name: 'shoppingCalendar',
6.     type: calendarManager.CalendarType.LOCAL,
7.     // 日历账户显示名称：建议使用应用实际名称。
8.     displayName: '购物'
9.   };
10.   // 日历配置信息
11.   const config: calendarManager.CalendarConfig = {
12.     // 设置日历账户颜色
13.     color: '#aabbcc'
14.   };
15.   const startTime = new Date('2025-12-19T19:00:00').getTime();
16.   const endTime = new Date('2025-12-19T20:00:00').getTime();
17.   // 日程配置信息
18.   const event: calendarManager.Event = {
19.     type: calendarManager.EventType.NORMAL,
20.     title: '购物节预热',
21.     startTime: startTime,
22.     endTime: endTime,
23.     isAllDay: false,
24.     reminderTime: [0, 10],
25.     description: '9.9限时秒杀,还有精彩福利',
26.     // 一键服务
27.     service: {
28.       type: calendarManager.ServiceType.SHOPPING,
29.       uri: 'demo://mobile/player?params='
30.     }
31.   }
32.   try {
33.     // 创建日历账户
34.     let data: calendarManager.Calendar | undefined= await calendarMgr?.createCalendar(calendarAccount);
35.     if (!data || data === null) {
36.       console.error('Failed to create calendar. data is null.');
37.       return;
38.     }
39.     // 请确保日历账户创建成功后，再进行相关日程的管理
40.     // 设置日历配置信息，设置日历账户颜色
41.     await data.setConfig(config);
42.     // 添加日程
43.     id = await data.addEvent(event);
44.     console.info(`Succeeded in creating calendar and event, result: ${JSON.stringify(id)}`);
45.   } catch (error) {
46.     console.error(`Failed to create calendar or event. Code: ${error.code}, message: ${error.message}`);
47.   }
48. }

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163618.40800007503291255216183351363845:50001231000000:2800:3A060A6D78BAC590E75B0F98CD9BDCDD67699BA4F838E1D8831BC7D3F18524AB.png)

### 还款提醒场景

下表列出了该场景中主要字段的推荐配置及其说明：

|字段名称|对应设置项|建议取值|
|:--|:--|:--|
|日程标题|title|还款提醒|
|开始时间|startTime|还款日日期|
|结束时间|endTime|还款日日期|
|全天日程|isAllDay|true：表示添加全天日程。|
|提醒时间|reminderTime|0：全天日程时表示当天上午9点提醒（非全天日程则是日程开始时间）。<br><br>不填时，默认为不提醒。|
|日历账户（在日历中对用户体现）|displayName|生态应用名（建议与应用市场中名称一致）|
|备注|description|可补充待还款金额信息|
|一键服务|ServiceType|calendarManager.ServiceType.Repayment|

创建日程示例和示意图如下：

1. // Index.ets
2. async createRepaymentCalendarAndEvent(): Promise<void> {
3.   // 指定日历账户信息
4.   const calendarAccount: calendarManager.CalendarAccount = {
5.     name: 'repaymentCalendar',
6.     type: calendarManager.CalendarType.LOCAL,
7.     // 日历账户显示名称：建议使用应用实际名称。
8.     displayName: '金融理财'
9.   };
10.   // 日历配置信息
11.   const config: calendarManager.CalendarConfig = {
12.     // 设置日历账户颜色
13.     color: '#aabbcc'
14.   };
15.   const startTime = new Date('2025-10-20T00:00:00').getTime();
16.   const endTime = new Date('2025-10-20T23:59:59').getTime();
17.   // 日程配置信息
18.   const event: calendarManager.Event = {
19.     type: calendarManager.EventType.NORMAL,
20.     title: '还款提醒',
21.     startTime: startTime,
22.     endTime: endTime,
23.     isAllDay: true,
24.     // 全天日程时，提醒时间为0表示当天上午9点提醒
25.     reminderTime: [0],
26.     description: '本月账单：待还款10989.35元',
27.     // 一键服务
28.     service: {
29.       type: calendarManager.ServiceType.REPAYMENT,
30.       uri: 'demo://mobile/player?params='
31.     }
32.   }
33.   try {
34.     // 创建日历账户
35.     let data: calendarManager.Calendar | undefined= await calendarMgr?.createCalendar(calendarAccount);
36.     if (!data || data === null) {
37.       console.error('Failed to create calendar. data is null.');
38.       return;
39.     }
40.     // 请确保日历账户创建成功后，再进行相关日程的管理
41.     // 设置日历配置信息，设置日历账户颜色
42.     await data.setConfig(config);
43.     // 添加日程
44.     id = await data.addEvent(event);
45.     console.info(`Succeeded in creating calendar and event, result: ${JSON.stringify(id)}`);
46.   } catch (error) {
47.     console.error(`Failed to create calendar or event. Code: ${error.code}, message: ${error.message}`);
48.   }
49. }

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163618.57265742134467113257476572954933:50001231000000:2800:670482BC9A7E7259BAA35056728B49051DACEA0427005F4E6FB8EDDFE031F79E.png)

### 课程提醒场景

下表列出了该场景中主要字段的推荐配置及其说明：

|字段名称|对应设置项|建议取值|
|:--|:--|:--|
|日程标题|title|课程名称|
|开始时间|startTime|课程开始时间|
|结束时间|endTime|课程结束时间|
|提醒时间|reminderTime|准时、10分钟前分别提醒|
|日历账户（在日历中对用户体现）|displayName|生态应用名（建议与应用市场中名称一致）|
|备注|description|可补充课程相关介绍|
|一键服务|ServiceType|calendarManager.ServiceType.Class|

创建日程示例和示意图如下：

1. // Index.ets
2. async createClassCalendarAndEvent(): Promise<void> {
3.   // 指定日历账户信息
4.   const calendarAccount: calendarManager.CalendarAccount = {
5.     name: 'classCalendar',
6.     type: calendarManager.CalendarType.LOCAL,
7.     // 日历账户显示名称：建议使用应用实际名称。
8.     displayName: '我的课表'
9.   };
10.   // 日历配置信息
11.   const config: calendarManager.CalendarConfig = {
12.     // 设置日历账户颜色
13.     color: '#aabbcc'
14.   };
15.   const startTime = new Date('2025-11-03T09:00:00').getTime();
16.   const endTime = new Date('2025-11-03T09:45:00').getTime();
17.   // 日程配置信息
18.   const event: calendarManager.Event = {
19.     type: calendarManager.EventType.NORMAL,
20.     title: '语文课',
21.     startTime: startTime,
22.     endTime: endTime,
23.     isAllDay: false,
24.     reminderTime: [0, 10],
25.     description: '语文课上课前准备诗歌朗读',
26.     // 一键服务
27.     service: {
28.       type: calendarManager.ServiceType.CLASS,
29.       uri: 'demo://mobile/player?params='
30.     }
31.   }
32.   try {
33.     // 创建日历账户
34.     let data: calendarManager.Calendar | undefined= await calendarMgr?.createCalendar(calendarAccount);
35.     if (!data || data === null) {
36.       console.error('Failed to create calendar. data is null.');
37.       return;
38.     }
39.     // 请确保日历账户创建成功后，再进行相关日程的管理
40.     // 设置日历配置信息，设置日历账户颜色
41.     await data.setConfig(config);
42.     // 添加日程
43.     id = await data.addEvent(event);
44.     console.info(`Succeeded in creating calendar and event, result: ${JSON.stringify(id)}`);
45.   } catch (error) {
46.     console.error(`Failed to create calendar or event. Code: ${error.code}, message: ${error.message}`);
47.   }
48. }

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163618.57999573823869260023351917145110:50001231000000:2800:A997D26875AADA2E25ED560A561D8F5C3640166A4F8B7BFC757BD213793F8554.png)

### 影音娱乐场景

下表列出了该场景中主要字段的推荐配置及其说明：

|字段名称|对应设置项|建议取值|
|:--|:--|:--|
|日程标题|title|赛事名称|
|开始时间|startTime|赛事开始时间|
|结束时间|endTime|赛事结束时间|
|提醒时间|reminderTime|准时、10分钟前分别提醒|
|日历账户（在日历中对用户体现）|displayName|生态应用名（建议与应用市场中名称一致）|
|备注|description|可补充赛事相关介绍|
|一键服务|ServiceType|calendarManager.ServiceType.SportsEvents|

创建日程示例和示意图如下：

1. // Index.ets
2. async createSportsCalendarAndEvent(): Promise<void> {
3.   // 指定日历账户信息
4.   const calendarAccount: calendarManager.CalendarAccount = {
5.     name: 'sportsEventsCalendar',
6.     type: calendarManager.CalendarType.LOCAL,
7.     // 日历账户显示名称：建议使用应用实际名称。
8.     displayName: '足球比赛'
9.   };
10.   // 日历配置信息
11.   const config: calendarManager.CalendarConfig = {
12.     // 设置日历账户颜色
13.     color: '#aabbcc'
14.   };
15.   const startTime = new Date('2025-10-19T20:00:00').getTime();
16.   const endTime = new Date('2025-10-19T21:30:00').getTime();
17.   // 日程配置信息
18.   const event: calendarManager.Event = {
19.     type: calendarManager.EventType.NORMAL,
20.     title: '2026年足球联赛',
21.     startTime: startTime,
22.     endTime: endTime,
23.     isAllDay: false,
24.     reminderTime: [0, 10],
25.     description: 'A组 xx队首战',
26.     // 一键服务
27.     service: {
28.       type: calendarManager.ServiceType.SPORTS_EVENTS,
29.       uri: 'demo://mobile/player?params='
30.     }
31.   }
32.   try {
33.     // 创建日历账户
34.     let data: calendarManager.Calendar | undefined= await calendarMgr?.createCalendar(calendarAccount);
35.     if (!data || data === null) {
36.       console.error('Failed to create calendar. data is null.');
37.       return;
38.     }
39.     // 请确保日历账户创建成功后，再进行相关日程的管理
40.     // 设置日历配置信息，设置日历账户颜色
41.     await data.setConfig(config);
42.     // 添加日程
43.     id = await data.addEvent(event);
44.     console.info(`Succeeded in creating calendar and event, result: ${JSON.stringify(id)}`);
45.   } catch (error) {
46.     console.error(`Failed to create calendar or event. Code: ${error.code}, message: ${error.message}`);
47.   }
48. }

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163618.98996446214904185689403077429796:50001231000000:2800:4BACE8E449E15EA97348E9522381286517855DAB49CC2BD195BAE4AB31786E6A.png)

### 运动训练场景

下表列出了该场景中主要字段的推荐配置及其说明：

|字段名称|对应设置项|建议取值|
|:--|:--|:--|
|日程标题|title|训练课程名称|
|开始时间|startTime|训练开始时间|
|结束时间|endTime|训练结束时间|
|提醒时间|reminderTime|准时、30分钟前分别提醒|
|日历账户（在日历中对用户体现）|displayName|生态应用名（建议与应用市场中名称一致）|
|备注|description|可补充训练计划相关介绍|
|一键服务|ServiceType|calendarManager.ServiceType.SportsExercise|

创建日程示例及示意图如下：

1. // Index.ets
2. async createSportsExerciseEvent(): Promise<void> {
3.   // 指定日历账户信息
4.   const calendarAccount: calendarManager.CalendarAccount = {
5.     name: 'sportsExerciseCalendar',
6.     type: calendarManager.CalendarType.LOCAL,
7.     // 日历账户显示名称：建议使用应用实际名称。
8.     displayName: '运动健康'
9.   };
10.   // 日历配置信息
11.   const config: calendarManager.CalendarConfig = {
12.     // 设置日历账户颜色
13.     color: '#aabbcc'
14.   };
15.   const startTime = new Date('2025-10-26T10:30:00').getTime();
16.   const endTime = new Date('2025-10-26T10:45:00').getTime();
17.   // 日程配置信息
18.   const event: calendarManager.Event = {
19.     type: calendarManager.EventType.NORMAL,
20.     title: '健身操·15分钟无跑跳燃脂',
21.     startTime: startTime,
22.     endTime: endTime,
23.     isAllDay: false,
24.     reminderTime: [0, 30],
25.     description: '训练日第17天',
26.     // 一键服务
27.     service: {
28.       type: calendarManager.ServiceType.SPORTS_EXERCISE,
29.       uri: 'demo://mobile/player?params='
30.     }
31.   }
32.   try {
33.     // 创建日历账户
34.     let data: calendarManager.Calendar | undefined= await calendarMgr?.createCalendar(calendarAccount);
35.     if (!data || data === null) {
36.       console.error('Failed to create calendar. data is null.');
37.       return;
38.     }
39.     // 请确保日历账户创建成功后，再进行相关日程的管理
40.     // 设置日历配置信息，设置日历账户颜色
41.     await data.setConfig(config);
42.     // 添加日程
43.     id = await data.addEvent(event);
44.     console.info(`Succeeded in creating calendar and event, result: ${JSON.stringify(id)}`);
45.   } catch (error) {
46.     console.error(`Failed to create calendar or event. Code: ${error.code}, message: ${error.message}`);
47.   }
48. }

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163618.56118128040447597309707735162311:50001231000000:2800:C2235374F597DF91667D56451E4E5866E63F1A18D9E79C95B022D07AB05E56CF.png)

### 会议场景

下表列出了该场景中主要字段的推荐配置及其说明：

|字段名称|对应设置项|建议取值|
|:--|:--|:--|
|日程标题|title|会议主题|
|开始时间|startTime|会议开始时间|
|结束时间|endTime|会议结束时间|
|与会人|attendee|与会人信息|
|提醒时间|reminderTime|准时、15分钟前分别提醒|
|日历账户（在日历中对用户体现）|displayName|生态应用名（建议与应用市场中名称一致）|
|备注|description|可补充会议相关介绍|
|一键服务|ServiceType|calendarManager.ServiceType.Meeting|

创建日程示例和示意图如下：

1. // Index.ets
2. async createMeetingEvent(): Promise<void> {
3.   // 指定日历账户信息
4.   const calendarAccount: calendarManager.CalendarAccount = {
5.     name: 'meetingCalendar',
6.     type: calendarManager.CalendarType.LOCAL,
7.     // 日历账户显示名称：建议使用应用实际名称。
8.     displayName: '会议'
9.   };
10.   // 日历配置信息
11.   const config: calendarManager.CalendarConfig = {
12.     // 设置日历账户颜色
13.     color: '#aabbcc'
14.   };
15.   // 与会人信息
16.   let attendee: calendarManager.Attendee[] = [
17.     {
18.       name: 'Chris',
19.       email: 'test1@xx.com',
20.       role: calendarManager.AttendeeRole.ORGANIZER
21.     },
22.     {
23.       name: 'Jack',
24.       email: 'test2@xx.com',
25.       role: calendarManager.AttendeeRole.PARTICIPANT,
26.       type: calendarManager.AttendeeType.REQUIRED
27.     },
28.     {
29.       name: 'Jerry',
30.       email: 'test3@xx.com',
31.       role: calendarManager.AttendeeRole.PARTICIPANT,
32.       type: calendarManager.AttendeeType.REQUIRED
33.     }
34.   ];
35.   const startTime = new Date('2025-10-20T09:00:00').getTime();
36.   const endTime = new Date('2025-10-20T10:00:00').getTime();
37.   // 日程配置信息
38.   const event: calendarManager.Event = {
39.     type: calendarManager.EventType.NORMAL,
40.     title: 'xxx会议',
41.     startTime: startTime,
42.     endTime: endTime,
43.     isAllDay: false,
44.     reminderTime: [0, 15],
45.     attendee: attendee,
46.     description: 'xx事务评审',
47.     // 一键服务
48.     service: {
49.       type: calendarManager.ServiceType.MEETING,
50.       uri: 'demo://mobile/player?params='
51.     }
52.   }
53.   try {
54.     // 创建日历账户
55.     let data: calendarManager.Calendar | undefined= await calendarMgr?.createCalendar(calendarAccount);
56.     if (!data || data === null) {
57.       console.error('Failed to create calendar. data is null.');
58.       return;
59.     }
60.     // 请确保日历账户创建成功后，再进行相关日程的管理
61.     // 设置日历配置信息，设置日历账户颜色
62.     await data.setConfig(config);
63.     // 添加日程
64.     id = await data.addEvent(event);
65.     console.info(`Succeeded in creating calendar and event, result: ${JSON.stringify(id)}`);
66.   } catch (error) {
67.     console.error(`Failed to create calendar or event. Code: ${error.code}, message: ${error.message}`);
68.   }
69. }

![](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20251216163618.09903733925192118662120818802111:50001231000000:2800:CCB9ECEB19F0773C2876AAA9A82A8C88B51034640D2DAC03B9565EC047BF7956.png)

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/calendar-service "注册并管理一键服务日程")
# Contacts Kit开发概述

更新时间: 2025-12-16 16:35

Contacts Kit可以帮助开发者轻松实现联系人的增删改查等功能。该Kit提供了一系列API，可以让开发者在应用中快速集成联系人管理功能。

详情请参考[@ohos.contact API](https://developer.huawei.com/consumer/cn/doc/harmonyos-references/js-apis-contact)。

## 能力范围

通过Contacts Kit，开发者可以对联系人进行管理，包括增加、删除、修改、查询联系人信息。开发者还可以通过Picker的方式，拉起联系人列表。

面向所有应用开放如下能力：

- [使用Picker选择联系人](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/contacts-intro#%E4%BD%BF%E7%94%A8picker%E9%80%89%E6%8B%A9%E8%81%94%E7%B3%BB%E4%BA%BA)

面向三方应用受限开放如下能力：

注意

当前能力受限开放，需要申请受限开放权限ohos.permission.READ_CONTACTS或ohos.permission.WRITE_CONTACTS。该权限通常不允许三方应用申请，仅符合[指定场景](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/restricted-permissions#ohospermissionread_contacts)的应用可申请该权限。

申请方式请参考：[申请使用受限权限](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/declare-permissions-in-acl)。

- [联系人管理](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/contacts-intro#%E8%81%94%E7%B3%BB%E4%BA%BA%E7%AE%A1%E7%90%86%E5%8F%97%E9%99%90%E5%BC%80%E6%94%BE)

## 使用Picker选择联系人

当用户选择联系人的时候，通过Picker的方式，拉起联系人列表，引导用户完成界面操作，接口本身无需申请权限。

1. 导入相关的联系人模块。
    
    1. import { contact } from '@kit.ContactsKit';
    2. import { BusinessError } from '@kit.BasicServicesKit';
    
2. 调用联系人接口，拉起联系人列表，用户点击对应的联系人后返回。
    
    1. contact.selectContacts({
    2.   isMultiSelect:false
    3. },(err: BusinessError, data) => {
    4.     if (err) {
    5.       console.error('selectContact callback, errCode:' + err.code + ', errMessage:' + err.message);
    6.         return;
    7.     }
    8.     console.info(`selectContact callback: success data->${JSON.stringify(data)}`);
    9. });
    
3. 完成操作，返回想要的data数据。
    

## 联系人管理（受限开放）

若需要在应用内实现管理联系人的功能，可以使用permissions接口获取应用对联系人的编辑权限。

1. 声明接口调用所需要的权限。
    
    当前能力受限开放，需要申请受限开放权限ohos.permission.WRITE_CONTACTS。该权限通常不允许三方应用申请，仅符合[指定场景](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/restricted-permissions#ohospermissionwrite_contacts)的应用可申请该权限。申请方式请参考：[申请使用受限权限](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/declare-permissions-in-acl)。
    
2. 设置一个需要的Permissions数组变量。
    
3. 执行对应联系人的权限操作。
    

4. // 示例代码
5. import { common, abilityAccessCtrl, Permissions, PermissionRequestResult } from '@kit.AbilityKit';
6. import { contact } from '@kit.ContactsKit';
7. import { BusinessError } from '@kit.BasicServicesKit';

8. @Entry
9. @Component
10. struct Contact {
11.   addContactByPermissions() {
12.     // 在组件内获取context，确保this.getUIContext().getHostContext()返回结果为UIAbilityContext
13.     let context = this.getUIContext().getHostContext() as common.UIAbilityContext;
14.     const permissions: Array<Permissions> = ['ohos.permission.WRITE_CONTACTS'];
15.     const contactInfo: contact.Contact = {
16.       name: { fullName: '王小明' },
17.       phoneNumbers: [{ phoneNumber: '13912345678' }]
18.     }
19.     abilityAccessCtrl.createAtManager().requestPermissionsFromUser(context, permissions).then((result: PermissionRequestResult) => {
20.       if (result.authResults[0] !== 0) { // 0 表示请求权限成功，其他任何非零值表示请求失败
21.         console.error('request contact permissions failed');
22.         return;
23.       }
24.       contact.addContact(context, contactInfo).then((data) => {
25.         console.info(`Succeeded in adding Contact. data: ${JSON.stringify(data)}`);
26.       }).catch((err: BusinessError) => {
27.         console.error(`Failed to add Contact. Code: ${err.code}, message: ${err.message}`);
28.       });
29.     })
30.   }

31.   build() {
32.     Row() {
33.       Column() {
34.         Button('添加联系人')
35.           .onClick(() => {
36.             this.addContactByPermissions();
37.           })
38.       }
39.       .width('100%')
40.     }
41.     .height('100%')
42.   }
43. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/contacts-kit "Contacts Kit（联系人服务）")
# 使用picker管理联系人

更新时间: 2025-12-16 16:36

## 接口说明

|接口名|描述|
|:--|:--|
|addContactViaUI(context: Context, contact: Contact): Promise<number>|调用新建联系人接口，打开新建联系人UI界面，新建完成。使用Promise异步回调。|
|saveToExistingContactViaUI(context: Context, contact: Contact): Promise<number>|调用保存至已有联系人接口，选择联系人UI界面并完成编辑。使用Promise异步回调。|

## 使用picker新建联系人

调用新建联系人接口，打开新建联系人UI界面，用户可在UI界面中填写并新建联系人。

1. import { common } from '@kit.AbilityKit';
2. import { contact } from '@kit.ContactsKit';
3. import { BusinessError } from '@kit.BasicServicesKit';

4. @Entry
5. @Component
6. struct Index {
7.   @State message: string = 'Hello World';

8.   build() {
9.     Column() {
10.       Text(this.message)
11.         .fontSize(50)
12.         .fontWeight(FontWeight.Bold)
13.         .onClick(() => {
14.           let contactInfo: contact.Contact = {
15.             name: {
16.               fullName: 'xxx'
17.             },
18.             phoneNumbers: [{
19.               phoneNumber: '138xxxxxx'
20.             }]
21.           }
22.           let context = this.getUIContext().getHostContext() as common.UIAbilityContext;
23.           let promise = contact.addContactViaUI(context, contactInfo);
24.           promise.then((data) => {
25.               console.info(`Succeeded in add Contact via UI.data->${JSON.stringify(data)}`);
26.             }).catch((err: BusinessError) => {
27.               console.error(`Failed to add Contact via UI. Code: ${err.code}, message: ${err.message}`);
28.             });
29.         })
30.     }
31.   }
32. }

## 使用picker更新联系人信息

可以通过拉起picker，将选中的联系人信息更新到现有联系人中。

1. import { common } from '@kit.AbilityKit';
2. import { contact } from '@kit.ContactsKit';
3. import { BusinessError } from '@kit.BasicServicesKit';

4. @Entry
5. @Component
6. struct Index {
7.   @State message: string = 'Hello World';

8.   build() {
9.     Column() {
10.       Text(this.message)
11.         .fontSize(50)
12.         .fontWeight(FontWeight.Bold)
13.         .onClick(() => {
14.           let contactInfo: contact.Contact = {
15.             id: 1,
16.             name: {
17.               fullName: 'xxx'
18.             },
19.             phoneNumbers: [{
20.               phoneNumber: '138xxxxxx'
21.             }]
22.           }
23.           let context = this.getUIContext().getHostContext() as common.UIAbilityContext;
24.           let promise = contact.saveToExistingContactViaUI(context, contactInfo);
25.           promise.then((data) => {
26.               console.info(`Succeeded in save to existing Contact via UI.data->${JSON.stringify(data)}`);
27.             }).catch((err: BusinessError) => {
28.               console.error(`Failed to save to existing Contact via UI. Code: ${err.code}, message: ${err.message}`);
29.             });
30.         })
31.     }
32.   }
33. }

[  
](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/contacts-intro "Contacts Kit开发概述")
