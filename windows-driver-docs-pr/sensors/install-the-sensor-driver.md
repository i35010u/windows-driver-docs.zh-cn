---
title: 安装传感器驱动程序
description: 本主题演示如何开发板上安装传感器驱动程序。
ms.assetid: 01CC1903-A36B-4ECC-856D-6196EC606973
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cda94f5dc8955bce05a900764d818c967f15779c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345256"
---
# <a name="install-the-sensor-driver"></a>安装传感器驱动程序


本主题演示如何在开发板上安装传感器驱动程序后更新辅助系统描述表 (SSDT) 的开发板。

本主题使用 Shark Cove 开发板和 ADXL345 加速感应器作为案例研究，以帮助解释开发板上安装传感器驱动程序的过程。 因此如果你想要执行本主题中介绍的任务，您必须首先在 Shark Cove 上安装操作系统。 有关如何执行此操作的详细信息，请参阅[下载适用于 Windows 10 的工具包和工具](https://docs.microsoft.com/windows-hardware/get-started/adk-install)，并按照说明安装 Windows 10。

在完成上 Shark Cove，请参阅安装操作系统后[生成传感器驱动程序](build-the-sensor-driver.md)若要了解如何构建在 Microsoft Visual Studio 中的驱动程序。 然后返回此处继续。

加速感应器附加到通过 I2C 总线 Shark Cove。 通过高级配置和电源接口 (ACPI) 枚举连接到 I2C 总线的外围设备。 因此加速感应器的示例驱动程序开发而不是插支持 ACPI。

若要使 Shark Cove ACPI 驱动程序的新设备 （加速感应器） 注意 I2C 总线上，必须将加速感应器有关的信息添加到 Shark Cove 在 SSDT 中。 下表描述的硬件资源和中断要求的硬件平台的设备，包括连接的外围设备，加速感应器等。

## <a name="before-you-begin"></a>开始之前


在开始执行如下所述的任务之前，请确保确认 Shark Cove 设置下图中所示：

![建议的安装 shark cove 板](images/sharkscove-setup.png)

## <a name="retrieve-and-review-the-default-ssdt"></a>检索和查看默认的 SSDT


本部分演示如何使用 ACPI 源语言 (ASL) 编译器将为 Shark Cove，检索工厂默认 SSDT，然后查看它。 您将学习如何使用已更新替换默认的 SSDT。

1. 在开发计算机上导航到要复制 ASL 编译器的以下位置： **c:\\Program Files (x86)\\Windows 工具包\\10\\工具\\x86\\ACPIVerify**
2. 复制*Asl.exe*文件，并将其保存到闪存驱动器。

3. 在 Shark Cove 上, 创建**工具**文件夹的根目录中。 然后将闪存驱动器附加到 Shark Cove USB 集线器，并复制*Asl.exe*的文件**工具**文件夹。

4. 打开命令提示符窗口，以管理员身份，并输入以下命令： **cd\\工具**
**dir**请确保*Asl.exe*在目录中列出文件。

5. 调用 ASL 编译器和 ASL 文件创建通过输入以下命令： **asl /tab = ssdt**
6. 请确保 ASL 文件已成功创建，可以通过输入以下命令： **dir ssdt.asl**
7. 在记事本中打开 ASL 文件，通过输入以下命令：**记事本 ssdt.asl**查看 ASL 文件，并请注意，没有到加速感应器或 I2C 总线的引用。

8. 关闭记事本。 然后输入以下命令，在命令提示符窗口中，若要重命名*ssdt.asl*文件。
**ren ssdt.asl ssdt old.asl**然后使用**dir**命令，确保该文件现在作为列出*ssdt old.asl*。

## <a name="update-the-default-ssdt"></a>更新默认 SSDT


执行以下任务来更新 SSDT，并将其替换工厂默认版本加载。 已更新的 SSDT 将存储在内存中，调用推迟*电池供电 RAM*。 因此请确保与 Shark Cove 一起提供的按钮单元格 （电池） 插入其套接字。

1. 复制以下更新的 SSDT 并将其粘贴到记事本的新实例。

    ```cpp
    // CreatorID=INTL  CreatorRev=20.14.805
    // FileLength=177   FileChkSum=0x88
    DefinitionBlock("SSDT.AML", "SSDT", 0x01, "Intel_", "ADebTabl", 0x00001000)
    {
        Scope()
        {
           Name(DPTR, 0x3bf2d000)
           Name(EPTR, 0x3bf3d000)
           Name(CPTR, 0x3bf2d010)
           Mutex(MMUT, 0x0)
           Method(MDBG, 0x1, Serialized)
           {
                Store(Acquire(MMUT, 0x3e8), Local0)
                If(LEqual(Local0, Zero))
                {
                    OperationRegion(ABLK, SystemMemory, CPTR, 0x10)
                    Field(ABLK, ByteAcc, NoLock, Preserve)
                    {
                        AAAA, 128
                    }
                    Store(Arg0, AAAA)
                    Add(CPTR, 0x10, CPTR)
                    If(LNot(LLess(CPTR, EPTR)))
                    {
                        Add(DPTR, 0x10, CPTR)
                    }
                    Release(MMUT)
                }
                Return(Local0)
            }
        }  
        Scope(_SB_)
        {
            Device(SPBA)
            {
                Name(_HID, "ADXL345Acc")
                Name(_UID, 1)
                Method(_CRS, 0x0, NotSerialized)
                {
                    Name(RBUF, ResourceTemplate()
                    {
                        I2CSerialBus(0x53, ControllerInitiated, 400000, 
                            AddressingMode7Bit, "\\_SB.I2C3", 0, ResourceConsumer)
                        GpioInt(Edge, ActiveHigh, Exclusive, PullDown, 0, "\\_SB.GPO2") 
                        {0x17}
                    })
                Return(RBUF)
                }
               Method(_DSM, 0x4, NotSerialized)
               {
                   If(LEqual(Arg0, Buffer(0x10)
                   {
                       0x1e, 0x54, 0x81, 0x76, 0x27, 0x88, 0x39, 0x42, 0x8d, 
                       0x9d, 0x36, 0xbe, 0x7f, 0xe1, 0x25, 0x42
                   }))
                   {
                       If(LEqual(Arg2, Zero))
                       {
                           Return(Buffer(One)
                           {
                               0x03
                           })
                       }
                       If(LEqual(Arg2, One))
                       {
                           Return(Buffer(0x4)
                           {
                               0x00, 0x01, 0x02, 0x03
                           })
                       }
                   }
                   Else
                   {
                       Return(Buffer(One)
                       {
                           0x00
                       })
                   }
                } // Method(_DSM ...)
            } // Device(SPBA)
        } // Scope(_SB_)
    }
    ```

2. 在记事本中，单击**文件** &gt; **另存为**。 然后单击**另存为类型**下拉列表中，然后选择**的所有文件**。

3. 在中**文件名**框中，键入*ssdt.asl*，然后单击**保存**，并关闭记事本。

4. 在命令提示符窗口中，使用**dir**命令，确保您可以看到默认的文件现在列为*ssdt old.asl*，并为列出的新文件*ssdt.asl*。

5. 编译*ssdt.asl*成 Shark Cove 通过输入以下命令可以理解的格式的文件： **asl ssdt.asl**
6. 验证是否已编译的文件已成功创建在**第 3 步**通过输入以下命令： **dir ssdt.aml**应会看到*ssdt.aml*工具中列出的文件目录。

7. 将已编译的文件加载到电池供电的 RAM，通过输入以下命令： **asl /loadtable ssdt.aml**
## <a name="turn-on-testsigning"></a>启用 testsigning


安装示例传感器驱动程序之前，必须启用 testsigning。 执行以下任务来启用 testsigning。 执行以下步骤安装传感器驱动程序通过**设备管理器**。

1. 在命令提示符窗口中，输入以下命令以查看是否 testsigning 已打开。<br/>
**bcdedit /enum**
2. 如果看到类似于下面的列表，其值设置为显示 testsigning 的条目`yes`然后跳到**第 5 步**。<br/>
![显示 testsigning 设置为是命令提示符窗口。](images/testsigning.png)

3. 如果你需要启用测试签名，然后输入以下命令： **bcdedit /set testsigning 上**

4. 重复**第 1 步**（在此练习中） 来验证 testsigning 系统变量的值现在设置为是 Windows 启动加载程序列表中。

5. 重新启动 Shark Cove。 看板重新启动，如保留约 2 秒，卷向上按钮输入系统安装程序 (UEFI) 窗口。

6. 在 UEFI 窗口中，选择**设备管理器** &gt; **System 安装程序** &gt; **启动**，并确保选中**UEFI 安全引导**设置为**&lt;禁用&gt;**。

7. 保存所做的更改并退出 UEFI 窗口。

## <a name="install-the-sensor-driver"></a>安装传感器驱动程序


有四种主要的 Shark Cove 板上安装驱动程序方法：

-   从网络源到 Shark Cove 上直接下载该驱动程序。
-   使用作为预配客户端连接你 Shark Cove 开发的主机计算机上，传感器驱动程序。 然后，部署到 Shark Cove 驱动程序从主计算机。
-   将驱动程序包复制到闪存驱动器，并将闪存驱动器附加到 Shark Cove。 然后，使用**devcon**命令从命令提示符窗口，若要手动安装驱动程序。
-   将驱动程序包复制到闪存驱动器，并将闪存驱动器附加到 Shark Cove。 然后安装该驱动程序通过手动**设备管理器**。

为简单起见，我们将使用前面的列表中的最后一个方法。 执行以下步骤手动安装传感器驱动程序通过**设备管理器**。

在安装传感器驱动程序之前，您必须连接到 Shark Cove 传感器。 璝惠 э ADXL345 加速感应器专题板从 SparkFun，若要获取其可用于示例传感器驱动程序，请参阅[准备在传感器测试板](prepare-your-sensor-test-board.md)。 有关如何将传感器专题开发板连接到 Shark Cove 的信息，请参阅[传感器连接到 Shark Cove 板](connect-your-sensor-to-the-sharks-cove-board.md)。

1. 请确保 ADXL345 加速感应器已连接到 Shark Cove J1C1 连接器，然后打开 Shark Cove 的电源。

2. 附加到供电的 USB 集线器连接到 Shark Cove 传感器驱动程序的闪存驱动器。 例如，这可以是保存生成的执行中的步骤的驱动程序的闪存驱动器[生成传感器驱动程序](build-the-sensor-driver.md)。

3. 打开**设备管理器**，并为"未知设备"查找**其他设备**节点具有一个黄色感叹号符号对其 （请参阅下面的屏幕截图）。<br/>![设备管理器显示的屏幕截图，显示黄色感叹号的未知的设备。](images/dev-manager.png)

4. 使用黄色惊叹号 （作为未知设备列出），右键单击该设备，然后选择**更新驱动程序软件**，然后单击**浏览计算机以查找驱动程序软件**。

5. 浏览到 ADXL345 驱动程序在闪存驱动器，然后单击**下一步**。 按照屏幕提示操作以安装传感器驱动程序。

6. 示例传感器驱动程序已成功安装后，**设备管理器**显示传感器，如以下屏幕截图中所示。<br/>![设备管理器屏幕截图，显示已成功安装的 adxl345 加速感应器的设备节点](images/dev-mgr-sensors.png)

有关如何使用 Visual Studio 将部署到客户端计算机 （例如 Shark Cove 中) 的驱动程序的信息，请参阅[部署到测试计算机的驱动程序](https://docs.microsoft.com/windows-hardware/drivers/develop/deploying-a-driver-to-a-test-computer)。

已成功安装后的示例传感器驱动程序，请参阅[测试通用传感器驱动程序](test-your-universal-sensor-driver.md)有关如何测试传感器信息。

 

 




