---
title: PnPUtil 示例
description: PnPUtil 示例
ms.date: 01/31/2018
ms.localizationpriority: medium
ms.openlocfilehash: d80a0f4ddcf91d247a73bc46362a8b8ad70849e7
ms.sourcegitcommit: 022dc99fdf23dc3501a3cebeb3c0698d504e31c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/13/2021
ms.locfileid: "107325036"
---
# <a name="pnputil-examples"></a>PnPUtil 示例

本主题提供有关如何使用 PnPUtil 工具的示例。

<dl>
  <dt>添加驱动程序包</dt>
  <dd><pre><code>pnputil /add-driver x:\driver.inf                                  </code></pre></dd>
  <dt>添加多个驱动程序包</dt>
  <dd><pre><code>pnputil /add-driver c:\oem\*.inf                                   </code></pre></dd>
  <dt>添加并安装驱动程序包</dt>
  <dd><pre><code>pnputil /add-driver device.inf /install                            </code></pre></dd>
  <dt>枚举 OEM 驱动程序包</dt>
  <dd><pre><code>pnputil /enum-drivers                                              </code></pre></dd>
  <dt>删除驱动程序包</dt>
  <dd><pre><code>pnputil /delete-driver oem0.inf                                    </code></pre></dd>
  <dt>强制删除驱动程序包</dt>
  <dd><pre><code>pnputil /delete-driver oem1.inf /force                             </code></pre></dd>
  <dt>导出驱动程序包</dt>
  <dd><pre><code>pnputil /export-driver oem6.inf .                                  </code></pre></dd>
  <dt>导出所有驱动程序包</dt>
  <dd><pre><code>pnputil /export-driver * c:\backup                                 </code></pre></dd>
  <dt>禁用设备实例 ID 指定的设备</dt>
  <dd><pre><code>pnputil /disable-device "USB\VID_045E&PID_00DB\6&870CE29&0&1"      </code></pre></dd>
  <dt>启用设备实例 ID 指定的设备</dt>
  <dd><pre><code>pnputil /enable-device "USB\VID_045E&PID_00DB\6&870CE29&0&1"       </code></pre></dd>
  <dt>重新启动设备实例 ID 指定的设备</dt>
  <dd><pre><code>pnputil /restart-device "USB\VID_045E&PID_00DB\6&870CE29&0&1"      </code></pre></dd>
  <dt>删除设备实例 ID 指定的设备</dt>
  <dd><pre><code>pnputil /remove-device "USB\VID_045E&PID_00DB\6&870CE29&0&1"       </code></pre></dd>
  <dt>扫描系统中的任何设备硬件更改</dt>
  <dd><pre><code>pnputil /scan-devices                                              </code></pre></dd>
  <dt>仅枚举系统上连接的设备</dt>
  <dd><pre><code>pnputil /enum-devices /connected                                   </code></pre></dd>
  <dt>枚举具有特定实例 ID 的设备</dt>
  <dd><pre><code>pnputil /enum-devices /instanceid "ACPI\PNP0A08\1"                 </code></pre></dd>
  <dt>枚举具有特定类的所有设备</dt>
  <dd><pre><code>pnputil /enum-devices /class Display                               </code></pre></dd>
  <dt>枚举具有特定问题代码的所有设备</dt>
  <dd><pre><code>pnputil /enum-devices /problem 28                                  </code></pre></dd>
  <dt>枚举出现问题的所有设备并显示硬件/兼容 Id</dt>
  <dd><pre><code>pnputil /enum-devices /problem /ids                                </code></pre></dd>
  <dt>仅枚举系统上已启用的接口</dt>
  <dd><pre><code>pnputil /enum-interfaces /enabled                                  </code></pre></dd>
</dl>


 

 





