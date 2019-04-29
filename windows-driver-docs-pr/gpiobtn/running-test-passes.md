---
title: 运行测试通过
description: MITT 平台可以提供测试自动化和选择自定义发送目标调查的 GPIO 模式测试 GPIO 按钮。
ms.assetid: E24AD015-1E14-4EF9-8443-D0F38FA3321E
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 03235cd635ea5c5db9da6b9926867c05fe38ac6f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390430"
---
# <a name="running-test-passes"></a>运行测试通过


MITT 平台可以提供测试自动化和选择自定义发送目标调查的 GPIO 模式测试 GPIO 按钮。

MITT 测试工具的详细信息，请联系MittSupport@microsoft.com。

若要开始，请参阅[GPIO 测试中 MITT](https://msdn.microsoft.com/library/windows/hardware/dn919780)。 下载安装程序，解压缩其内容，并阅读**自述文件**有关该工具的一般概述的文件。

## <a name="span-idend-to-endindicatortestingforconvertiblesspanspan-idend-to-endindicatortestingforconvertiblesspanspan-idend-to-endindicatortestingforconvertiblesspanend-to-end-indicator-testing-for-convertibles"></a><span id="End-to-end_indicator_testing_for_convertibles"></span><span id="end-to-end_indicator_testing_for_convertibles"></span><span id="END-TO-END_INDICATOR_TESTING_FOR_CONVERTIBLES"></span>测试双用型的端到端指示器


请务必执行端到端测试双用型公开以下几个方面中的任何潜在问题的指示器：

-   将系统从一种模式转换为另一种模式时的各种计时。
-   可转换的机械具体信息。

### <a name="span-idlaptoptoslateconversiontestscenariospanspan-idlaptoptoslateconversiontestscenariospanspan-idlaptoptoslateconversiontestscenariospanlaptop-to-slate-conversion-test-scenario"></a><span id="Laptop_to_slate_conversion_test_scenario"></span><span id="laptop_to_slate_conversion_test_scenario"></span><span id="LAPTOP_TO_SLATE_CONVERSION_TEST_SCENARIO"></span>向静态转换测试方案的便携式计算机

开始在便携式计算机模式下 （键盘操作） 系统。

1.  按窗口按钮以导航到**启动**。
2.  按使用键盘来启动以字母**搜索**。
3.  点击编辑字段中。 *验证*:不应部署在屏幕键盘。
4.  旋转系统 （横向与纵向）。 *验证*:系统应不会旋转。
5.  将从便携式计算机以平板转换 （键盘变得无法访问）。 此类操作的示例是： 旋转或翻转屏幕、 分离的键盘，等等。
6.  在点击**搜索**编辑字段。 *验证*:应部署在屏幕键盘。
7.  旋转系统 （横向与纵向）。 *验证*:系统应轮换。

**请注意**  为每个不同的方式可将系统转换为平板电脑模式重复这些步骤。

 

 

 




