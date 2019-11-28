# OpenCore I5-9500 B360N BCM94360CSAX（终章）

###### 2019-11-28

---

电脑是在今年（2019年）618之后自己在配的，所有零件（PCI-e网卡来自 TB ）均来自 JD 对比现在的价格有的涨了有的跌了，管它呢，反正已经用了好几个月而且用的开心。

不出意外的话这应该会是黑苹果折腾之路的最后一站，自此只要不出什么问题应该不会再继续折腾了。

## 配置及购买时价格

Wi-Fi网卡是后加的，因为定位、隔空投送、接力都必须使用Wi-Fi和蓝牙所以加了。

| 名称      | 型号              | 规格说明        | 数量 | 单价 |
| :------- | :--------------- | :------------- | --: | --: |
| CPU       | Intel I5-9500   | 3.0GHz 6核6线程 |  1   | 1609 |
| 主板      | 技嘉 B360N        | ITX            |  1   |  998 |
| 散热器    | IS-40X            | 9CM，高4.5CM   |  1   |   99 |
| 内存      | 芝奇 DDR4 2666    | 8GB            |  2   |  269 |
| 主硬盘    | Intel 760P M.2    | 256GB          |  1   |  309 |
| 副硬盘    | 三星 860 QVO      | 1TB             |  1   |  699 |
| 机箱      | 迎广 肖邦         | 自带150W电源      |  1   |  553 |
| 显示器    | BenQ PD2500Q      | 2K             |  1   | 1949 |
| 键鼠      | 雷柏 9300M        | 无线蓝牙套装      |  1   |  159 |
| Wi-Fi&BT  | BCM94360CSAX     | 3天线，蓝牙4.0   |  1   |  240 |
| Wi-Fi天线  | --               | 3天线，6DB      |  1   |   38 |

## 实现功能

- 跳过引导选择界面，直接进入Catalina，等待时间1秒。
- CPU——变频正常，侦测为 4 档变频，打了补丁。
- 声卡——ALC892，正常驱动（有瑕疵，后面板无声音输出，前面板耳机孔可以自动切换，正常使用），layout 我使用7，测试1也是可以的只是喜欢7。
- 显卡——正常，侦测硬件加速开启（DP输出），若使用HDMI输出（需要打补丁）会影响硬件加速，未解决，目前显示器为DP口，所以没有打HDMI补丁。
- 有线网络——正常，使用**[IntelMausi](https://github.com/acidanthera/IntelMausi)**驱动。
- 无线网络——正常，原生驱动，系统内可手动关闭及启用。
- 蓝牙——正常，原生驱动，系统内可手动关闭及启用。- 睡眠——正常。
- 显示——可开启HIDPI，目前直接使用2K输出。**[one-key-hidpi](https://github.com/xzhih/one-key-hidpi)**
- 隔空投送——正常。
- 接力——正常。

我使用的是Catalina，Windows10双系统，各自使用一块硬盘，独立的EFI引导，切换系统直接冷启用F12切换，Wi-Fi网卡也相对独立，没有拆板载WI-FI&蓝牙，Windows使用Intel CNVi（AC9462），禁用BCM94360；Catalina使用BCM94360，屏蔽掉Intel CNVi蓝牙就可以了，因为从Windows切换到Catalina Intel 蓝牙实际是可以使用的，避免冲突直接屏蔽掉。

机型设置：很多教程都推荐集显使用Mac mini，我使用macmini8,1。

附件中的序列号等信息已清除，请自行添加。只需要MLB，ROM，SystemSerialNumber，SystemUUID即可。可以使用CloverConfigurator生成。

## BIOS设置

B360N没有CFG-Lock选项，没有原生NVRAM。

- Save & Exit → **Load Optimized Defaults**
- BIOS → **Windows 8/10 Features → Other OS**
- BIOS → **CSM Support → Disabled**
- BIOS → **Secure Boot → Secure Boot Enable → Disabled**
- Peripherals → **LEDs in System Power On State → Off**（关闭光污染，个人喜好）
- Peripherals → **USB Configuration → XHCI Hand-off → Enabled**
- Chipset → **VT-d → Disabled**
- Chipset → **Internal Graphics → Enabled**
- Chipset → **Above 4G Decoding → Enabled**
- Save & Exit → **Save & Exit Setup**

CFG-Lock **B360N需要借助工具才能修改** [教程地址](https://blog.xjn819.com/?p=317)

模拟NVRAM **B360N只能模拟NVRAM** [教程地址](https://blog.xjn819.com) 3.1 模拟NVRAM

*个人理解：NVRAM只有OC引导多系统是才有意义，像我这种使用多硬盘、独立引导的没有实际意义。*

## EFI文件夹结构

![EFI文件夹结构](http://microbox.xicp.cn/usr/uploads/2019/11/513934096.png)

    虽然定制了USB，目录中保留了USBInjectAll。

## Platforminfo获取

![Clover_Configurator_01](http://microbox.xicp.cn/usr/uploads/2019/11/3988654059.png)

![Clover_Configurator_02](http://microbox.xicp.cn/usr/uploads/2019/11/3880779242.png)

![Clover_Configurator_03](http://microbox.xicp.cn/usr/uploads/2019/11/902346226.png)

    把获取到的信息填写位置对应的位置：

![Platforminfo](http://microbox.xicp.cn/usr/uploads/2019/11/3871584907.png)

## 图片展示

![迎广肖邦](http://microbox.xicp.cn/usr/uploads/2019/11/1258166984.jpg)

    **自带150W静音电源，大小比A4还小**

![Benq PD2500Q](http://microbox.xicp.cn/usr/uploads/2019/11/3510382271.jpg)

    **2K分辨率，自带音箱**

![关于电脑](http://microbox.xicp.cn/usr/uploads/2019/11/1163905711.png)

![显卡](http://microbox.xicp.cn/usr/uploads/2019/11/2805890813.png)

![电源](http://microbox.xicp.cn/usr/uploads/2019/11/1041175763.png)

![蓝牙](http://microbox.xicp.cn/usr/uploads/2019/11/1595817141.png)

![音频](http://microbox.xicp.cn/usr/uploads/2019/11/2369819937.png)

![网络](http://microbox.xicp.cn/usr/uploads/2019/11/2144576307.png)

![Wi-Fi](http://microbox.xicp.cn/usr/uploads/2019/11/3968860506.png)

![Wi-Fi列表](http://microbox.xicp.cn/usr/uploads/2019/11/1594717205.png)

![隔空投送](http://microbox.xicp.cn/usr/uploads/2019/11/1338808556.png)

![节能](http://microbox.xicp.cn/usr/uploads/2019/11/1971198397.png)

    CPU打补丁之后开启了4项节能，要开启5项，需要加载PPMC以及LPCB下的PMCR才能出现。

![USB定制](http://microbox.xicp.cn/usr/uploads/2019/11/3262162489.png)

    后面板的type-c接口直接屏蔽，因为我没有那类型的设备。

![CFG-lock](http://microbox.xicp.cn/usr/uploads/2019/11/402382013.png)

![硬件加速](http://microbox.xicp.cn/usr/uploads/2019/11/3440977688.png)

## PCI-e转接卡改造

转接卡尺寸不能放入机箱中，切掉转接卡部分板材，顺利插入。

![转接卡](http://microbox.xicp.cn/usr/uploads/2019/11/2986096748.png)

    红色框线内的部分是我切除掉的部分，切割工艺太差就不贴图了。

![后面板](http://microbox.xicp.cn/usr/uploads/2019/11/1399325842.png)

    两套Wi-Fi蓝牙，互不影响。

## Config.plist

**特别提示：MLB，ROM，SystemSerialNumber，SystemUUID已清除，请自行添加。**

**特别提示：MLB，ROM，SystemSerialNumber，SystemUUID已清除，请自行添加。**

**特别提示：MLB，ROM，SystemSerialNumber，SystemUUID已清除，请自行添加。**
