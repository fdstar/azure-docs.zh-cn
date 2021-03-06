---
title: Azure TextBox UI 元素 | Microsoft Docs
description: 介绍了 Azure 门户的 Microsoft.Common.TextBox UI 元素。
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2018
ms.author: tomfitz
ms.openlocfilehash: 4238d241ec5daacd06485b118a8ccf9b68a9d6d9
ms.sourcegitcommit: e221d1a2e0fb245610a6dd886e7e74c362f06467
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/07/2018
---
# <a name="microsoftcommontextbox-ui-element"></a>Microsoft.Common.TextBox UI 元素
一个可用来编辑无格式文本的控件。

## <a name="ui-sample"></a>UI 示例
![Microsoft.Common.TextBox](./media/managed-application-elements/microsoft.common.textbox.png)

## <a name="schema"></a>架构
```json
{
  "name": "element1",
  "type": "Microsoft.Common.TextBox",
  "label": "Some text box",
  "defaultValue": "my value",
  "toolTip": "Use only allowed characters",
  "constraints": {
    "required": true,
    "regex": "^[a-z0-9A-Z]{1,30}$",
    "validationMessage": "Only alphanumeric characters are allowed, and the value must be 1-30 characters long."
  },
  "visible": true
}
```

## <a name="remarks"></a>备注
- 如果 `constraints.required` 设置为 **true**，则文本框必须包含值才能成功通过验证。 默认值为 **false**。
- `constraints.regex` 是一个 JavaScript 正则表达式模式。 如果指定，则文本框的值必须与模式完全匹配才能成功通过验证。 默认值为 **null**。
- `constraints.validationMessage` 是当文本框的值未通过验证时会显示的一个字符串。 如果未指定，则会使用文本框的内置验证消息。 默认值为 **null**。
- 当 `constraints.required` 设置为 **false** 时可以为 `constraints.regex` 指定值。 在这种情况下，文本框并非必须具有值才能成功通过验证。 如果指定了一个值，则它必须与正则表达式模式匹配。

## <a name="sample-output"></a>示例输出

```json
"my value"
```

## <a name="next-steps"></a>后续步骤
* 有关创建 UI 定义的简介，请参阅 [CreateUiDefinition 入门](create-uidefinition-overview.md)。
* 有关 UI 元素中的公用属性的说明，请参阅 [CreateUiDefinition 元素](create-uidefinition-elements.md)。
