---
title: 安装传感器驱动程序
description: 本主题说明如何在开发板上安装传感器驱动程序。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b03c37770f18cbcba1b2006e898095623cf735f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830995"
---
# <a name="install-the-sensor-driver"></a>安装传感器驱动程序


本主题说明如何在开发板上安装传感器驱动程序，并在为开发面板 (SSDT) 更新辅助系统说明表后安装该驱动程序。

本主题使用带 Cove 开发板和 ADXL345 加速感应器作为案例研究，以帮助说明在开发板上安装传感器驱动程序的过程。 因此，如果要执行本主题中所述的任务，必须先在带 Cove 上安装操作系统。 有关如何执行此操作的详细信息，请参阅 [下载适用于 windows 10 的工具包和工具](/windows-hardware/get-started/adk-install)，并按照说明安装 windows 10。

在带 Cove 上完成操作系统的安装后，请参阅 [构建传感器驱动程序](build-the-sensor-driver.md) 以了解如何在 Microsoft Visual Studio 中构建驱动程序。 然后返回此处继续。

加速感应通过 I2C 总线附加到带 Cove。 通过高级配置和电源接口 (ACPI) 枚举连接到 I2C 总线的外围网络。 因此，开发人员的示例驱动程序是为支持 ACPI 而不是即插即用而开发的。

若要使带 Cove 的 ACPI 驱动程序知道 (I2C 总线上的加速感应) ，则必须将有关该加速度的信息添加到带 Cove 上的 SSDT。 下表描述硬件平台设备的硬件资源和中断要求，包括与加速感应的连接外围设备。

## <a name="before-you-begin"></a>在开始之前


在开始执行下面所述的任务之前，请确保已设置带 Cove，如下图所示：

![建议用于带 cove 板的设置](images/sharkscove-setup.png)

## <a name="retrieve-and-review-the-default-ssdt"></a>检索和查看默认 SSDT


本部分演示如何使用 ACPI 源语言 (ASL) 编译器检索带 Cove 的出厂默认 SSDT，然后查看它。 你还将了解如何使用更新的 SSDT 替换默认值。

1. 在开发计算机上，导航到以下位置以将 ASL 编译器： **c： \\ Program 文件复制 (x86) \\ Windows 工具包 \\ 10 \\ Tools \\ x86 \\ ACPIVerify**
2. 复制 *Asl.exe* 文件，并将其保存到闪存驱动器。

3. 在带 Cove 上，在根目录中创建一个 " **工具** " 文件夹。 然后，将闪存驱动器连接到带 Cove 的 USB 集线器，并将 *Asl.exe* 文件复制到 " **Tools** " 文件夹中。

4. 以管理员身份打开命令提示符窗口，然后输入以下命令： **cd \\ 工具** 
 **目录** 确保 *Asl.exe* 文件列在目录中。

5. 通过输入以下命令调用 ASL 编译器并创建 ASL 文件： **ASL/tab = ssdt**
6. 输入以下命令，确保已成功创建 ASL 文件： **dir ssdt. ASL**
7. 输入以下命令，在记事本中打开 ASL 文件： **记事本 ssdt. ASL** 查看 ASL 文件，并且注意没有对加速感应程序或 I2C 总线的引用。

8. 关闭记事本。 然后，在命令提示符窗口中输入以下命令，重命名 *ssdt asl* 文件。
**ren ssdt. asl ssdt-old. asl** 然后，使用 **dir** 命令确保该文件现在列为 *ssdt-old. asl*。

## <a name="update-the-default-ssdt"></a>更新默认 SSDT


执行以下任务以更新 SSDT，并将其加载到替换出厂默认版本。 更新后的 SSDT 将存储在称为 *备有电池的 RAM* 的内存大中。 因此，请确保带 Cove 附带的按钮单元格 (电池) 插入其插槽中。

1. 复制以下已更新的 SSDT，并将其粘贴到记事本的新实例中。

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

2. 在记事本中，选择 " **文件** &gt; **另存为**"。 然后选择 " **保存类型** " 下拉框，并选择 " **所有文件**"。

3. 在 " **文件名" 框中** ，键入 *ssdt*，然后选择 " **保存**"，然后关闭记事本。

4. 在 "命令提示符" 窗口中，使用 **dir** 命令确保你可以看到现在作为 *ssdt-old* 列出的默认文件，并将新文件列为 *ssdt. asl*。

5. 通过输入以下命令，将 *ssdt asl* 文件编译为带 Cove 可以理解的格式： **asl ssdt. asl**
6. 通过输入以下命令验证是否已在 **步骤 3** 中成功创建已编译的文件： **dir ssdt** ，应会看到 "工具" 目录中列出的 *ssdt* 文件。

7. 输入以下命令，将编译后的文件加载到支持电池的 RAM 中： **asl/loadtable ssdt**
## <a name="turn-on-testsigning"></a>打开 testsigning


安装示例传感器驱动程序之前，必须打开 testsigning。 执行以下任务以打开 testsigning。 执行以下步骤，通过 **设备管理器** 安装传感器驱动程序。

1. 在 "命令提示符" 窗口中，输入以下命令，查看是否已打开 testsigning。<br/>
**bcdedit/enum**
2. 如果看到类似于下面的列表，则显示 testsigning 的条目，并将其值设置为， `yes` 然后跳到 **步骤 5**。<br/>
![显示 "testsigning" 设置为 "是" 的命令提示符窗口。](images/testsigning.png)

3. 如果需要启用测试签名，请输入以下命令： **bcdedit/set testsigning on**

4. 在本练习) 中重复 **步骤 1** (，验证 testsigning 系统变量的值现在是否在 Windows 启动加载程序列表中设置为 "是"。

5. 重新启动带 Cove。 在系统重新启动时，请将音量调高，使其保持约2秒，以输入系统设置 (UEFI) "窗口。

6. 在 UEFI 窗口中，选择 "**设备管理器** &gt; **系统安装程序** &gt; **启动**"，并确保将 " **UEFI 安全启动**" 设置为 " **&lt; 禁用 &gt;**"。

7. 保存更改并退出 UEFI 窗口。

## <a name="install-the-sensor-driver"></a>安装传感器驱动程序


在带 Cove 板上安装驱动程序的主要方法有四种：

-   直接从网络源将驱动程序下载到带 Cove。
-   在主计算机上开发传感器驱动程序，并将带 Cove 连接为预配的客户端。 然后将该驱动程序从主计算机部署到带 Cove。
-   将驱动程序包复制到闪存驱动器，并将闪存驱动器连接到带 Cove。 然后，在命令提示符窗口中使用 **devcon** 命令手动安装驱动程序。
-   将驱动程序包复制到闪存驱动器，并将闪存驱动器连接到带 Cove。 然后通过 **设备管理器** 手动安装驱动程序。

为简单起见，我们将使用上一列表中的最后一个方法。 执行以下步骤，通过 **设备管理器** 手动安装传感器驱动程序。

在安装传感器驱动程序之前，必须将传感器连接到带 Cove。 若要了解如何从 SparkFun 修改 ADXL345 加速器分类板，以使其使用示例传感器驱动程序，请参阅 [准备传感器测试板](prepare-your-sensor-test-board.md)。 若要了解如何将传感器分类板连接到带 Cove，请参阅 [将传感器连接到带 Cove](connect-your-sensor-to-the-sharks-cove-board.md)。

1. 请确保 ADXL345 加速感应连接到带 Cove J1C1 连接器，然后启动带 Cove。

2. 将带有传感器驱动程序的闪存驱动器连接到连接到带 Cove 的已通电 USB 集线器。 例如，这可以是闪存驱动器，你可以根据 [构建传感器驱动程序](build-the-sensor-driver.md)中的步骤来保存你构建的驱动程序。

3. 打开 **设备管理器**，并在 " **其他设备** " 节点中查找 "未知设备"，并在其上查找黄色惊叹号符号 (参见以下屏幕截图) 。<br/>![设备管理器屏幕截图，显示未知设备，并显示黄色感叹号。](images/dev-manager.png)

4. 选择并按住 (或右键单击) 设备，其中黄色惊叹号 (列为未知设备) ，选择 " **更新驱动程序软件**"，然后选择 **"浏览计算机以查找驱动程序软件**"。

5. 浏览到闪存驱动器上的 ADXL345 驱动程序，然后选择 " **下一步**"。 按照屏幕上的提示安装传感器驱动程序。

6. 成功安装示例传感器驱动程序后， **设备管理器** 显示传感器，如以下屏幕截图所示。<br/>![设备管理器屏幕截图，显示成功安装的 adxl345 加速感应器的设备节点](images/dev-mgr-sensors.png)

有关如何使用 Visual Studio 将驱动程序部署到客户端计算机 (如带 Cove) 的信息，请参阅将 [驱动程序部署到测试计算机](../develop/deploying-a-driver-to-a-test-computer.md)。

成功安装示例传感器驱动程序后，请参阅 [测试通用传感器驱动程序](test-your-universal-sensor-driver.md) ，了解有关如何测试传感器的信息。

 

