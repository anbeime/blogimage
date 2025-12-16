如何在鸿蒙系统使用ARKUI 颜色

在鸿蒙系统中使用ArkUI颜色，主要有以下几种方式：

**1. **使用内置主题颜色****

ArkUI提供了一套内置主题颜色，可通过`theme.colors`对象访问。这些颜色在不同主题模式（如浅色、深色）下会自动适配。

示例：

typescript

```typescript
import { theme } from '@kit.arkui';

@entry
@Component
struct MyComponent {
  build() {
    Column() {
      Text('一级文本').fontColor(theme.colors.fontPrimary);
      Text('二级文本').fontColor(theme.colors.fontSecondary);
      Row() {
        Text('品牌色').fontColor(theme.colors.brand);
        Text('警示色').fontColor(theme.colors.warning);
      }
    }
  }
}
```

**2. **自定义全局主题颜色****

若需自定义颜色，可创建自定义主题并应用到整个应用。

步骤如下：

1. **定义自定义颜色类**：

typescript

```typescript
// apptheme.ets
import { CustomColors, CustomTheme } from '@kit.arkui';

export class AppColors implements CustomColors {
  brand = 0xff75d9;        // 自定义品牌色
  fontPrimary = 0xffd53032; // 自定义一级文本颜色
  backgroundPrimary = 0xfff1f3f5; // 自定义一级背景色
}

export class AppTheme implements CustomTheme {
  public colors: AppColors = new AppColors();
}

export let gAppTheme: CustomTheme = new AppTheme();
```

2. **在Ability中设置全局主题**：

typescript

```typescript
// entryability.ets
import { ThemeControl } from '@kit.arkui';
import { gAppTheme } from './apptheme';

export default class EntryAbility extends UIAbility {
  onWindowStageCreate(windowStage: Window.WindowStage) {
    ThemeControl.setDefaultTheme(gAppTheme);
  }
}
```

**3. **局部应用自定义颜色****

在组件内部通过`withTheme`局部应用自定义主题，无需影响全局。

示例：

typescript

```typescript
@entry
@Component
struct MyPage {
  @State customTheme: CustomTheme = new AppTheme();

  build() {
    withTheme({ theme: this.customTheme }) {
      Column() {
        Text('局部应用主题').fontColor(theme.colors.fontPrimary);
        Button('切换主题').onClick(() => {
          // 切换自定义主题逻辑
        });
      }
    }
  }
}
```

**4. **直接使用颜色值****

可直接使用十六进制颜色值或RGB/RGBA格式定义颜色。

示例：

typescript

```typescript
Text('直接使用颜色').fontColor(0xff00ff00); // 绿色
Text('透明颜色').fontColor(Color.rgba(255, 0, 0, 0.5)); // 半透明红色
```

**5. **颜色渐变****

ArkUI支持线性渐变、角度渐变和径向渐变，适用于背景或特定组件。

示例（线性渐变）：

typescript

```typescript
Row() {
  .width(150)
  .height(150)
  .linearGradient({
    direction: GradientDirection.rightBottom,
    colors: [[0xffe1e1, 0.0], [0xd3e0dc, 0.3], [0xfcd1d1, 1.01]]
  })
}
```

通过以上方法，可在鸿蒙系统中灵活使用ArkUI颜色，实现丰富的视觉效果和主题适配。