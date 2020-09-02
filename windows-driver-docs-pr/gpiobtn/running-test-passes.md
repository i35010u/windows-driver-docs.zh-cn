---
title: 运行测试通过
description: MITT 平台通过提供测试自动化和用于自定义为目标调查发送的 GPIO 模式的选项来测试 GPIO 按钮。
ms.assetid: E24AD015-1E14-4EF9-8443-D0F38FA3321E
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 437fe9f2cd4d912b1a9ebc279c92a7deca2d18b5
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89381521"
---
# <a name="running-test-passes"></a>运行测试通过


MITT 平台通过提供测试自动化和用于自定义为目标调查发送的 GPIO 模式的选项来测试 GPIO 按钮。

有关 MITT 测试工具的详细信息，请联系 MittSupport@microsoft.com 。

若要开始，请参阅 [MITT 中的 GPIO 测试](../spb/gpio-tests-in-mitt.md)。 下载安装程序，解压缩其内容，并阅读 **自述** 文件以获取该工具的一般概述。

## <a name="span-idend-to-end_indicator_testing_for_convertiblesspanspan-idend-to-end_indicator_testing_for_convertiblesspanspan-idend-to-end_indicator_testing_for_convertiblesspanend-to-end-indicator-testing-for-convertibles"></a><span id="End-to-end_indicator_testing_for_convertibles"></span><span id="end-to-end_indicator_testing_for_convertibles"></span><span id="END-TO-END_INDICATOR_TESTING_FOR_CONVERTIBLES"></span>改装的端到端指示器测试


必须对改装执行端到端指示器测试，才能在以下领域公开任何潜在问题：

-   将系统从一种模式转换到另一种模式时的各种计时。
-   可转换的机械细节。

### <a name="span-idlaptop_to_slate_conversion_test_scenariospanspan-idlaptop_to_slate_conversion_test_scenariospanspan-idlaptop_to_slate_conversion_test_scenariospanlaptop-to-slate-conversion-test-scenario"></a><span id="Laptop_to_slate_conversion_test_scenario"></span><span id="laptop_to_slate_conversion_test_scenario"></span><span id="LAPTOP_TO_SLATE_CONVERSION_TEST_SCENARIO"></span>便携机到石板转换测试方案

以便携式计算机模式下的系统开始 (键盘可访问) 。

1.  按窗口按钮以导航到 " **开始**"。
2.  使用键盘按字母开始 **搜索**。
3.  在编辑字段中点击。 *验证*：屏幕键盘不应部署。
4.  将系统 (横向旋转到纵向，并向后) 。 *验证*：系统不应旋转。
5.  从便携式计算机转换为石板 (键盘将无法访问) 。 此类操作的示例包括：旋转或翻转屏幕、分离键盘等。
6.  在 **搜索** 编辑字段中点击。 *验证*：屏幕键盘应部署。
7.  将系统 (横向旋转到纵向，并向后) 。 *验证*：系统应旋转。

**注意**   对于系统可转换为平板电脑模式的每个不同方法，重复这些步骤。

 

 

