---
title: Matlab背景颜色修改
date: 2018-09-01 11:55:00
tags: [Matlab]
---


Matlab背景颜色修改

<!--more-->

## 背景
将`修改内容`添加到matlab的matlab.prf文件中，文件路径为在matlab中运行prefdir的结果,直接添加这些内容保存就好。 

## 操作
1， 在`matlab`命令行中运行`prefdir`， 获取`matlab.prf`文件所在路径

2， 打开`matlab.prf`所在路径， 找到`matlab.prf`文件， 作备份

3， 在新的`matlab.prf`中修改与`color`有关的属性

4，重启`matlab`，修改主题就完成了

## 主题选择
### 黑色主题
```
Editor.VariableHighlighting.Color=C-6931898
ColorsText=C-460558
Colors_M_SystemCommands=C-448910
Editorhighlight-lines=C-11974594
Colors_M_Warnings=C-27648
Colors_M_Strings=C-1647756
Editor.NonlocalVariableHighlighting.TextColor=C-5471745
Colors_HTML_HTMLLinks=C-16732805
Colors_M_Comments=C-8355712
Colors_M_Errors=C-65536
Colors_M_UnterminatedStrings=C-5111808
ColorsBackground=C-14211038
Colors_M_Keywords=C-10036753
Color_CmdWinWarnings=C-39936
ColorsMLintAutoFixBackground=C-7973573
Colors_M_Keywords=C-10036753
Editorhighlight-lines=C-13553108
Editorhighlight-caret-row-boolean-color=C-2167080


ColorsUseSystem=Bfalse
```

### 暖色主题
```
Color_CmdWinErrors=C-1703936
Color_CmdWinWarnings=C-39936
ColorsBackground=C-198941
ColorsMLintAutoFixBackground=C-1121868
ColorsText=C-16304574
ColorsUseMLintAutoFixBackground=Btrue
ColorsUseSystem=Bfalse
Colors_HTML_HTMLLinks=C-2935166
Colors_M_Comments=C-7167583
Colors_M_Errors=C-65536
Colors_M_Keywords=C-8021760
Colors_M_Strings=C-13983336
Colors_M_SystemCommands=C-3454186
Colors_M_UnterminatedStrings=C-5111808
Colors_M_Warnings=C-27648
Editor.NonlocalVariableHighlighting.TextColor=C-32640
Editor.VariableHighlighting.Color=C-7167583
EditorRightTextLimitLineColor=C-3355444

```

### darkmate
```
ColorsUseSystem=Bfalse
ColorsUseMLintAutoFixBackground=Btrue
Editor.VariableHighlighting.Automatic=Btrue
Editor.NonlocalVariableHighlighting=Btrue
EditorCodepadHighVisible=Btrue
EditorCodeBlockDividers=Btrue
Editorhighlight-caret-row-boolean=Btrue
EditorRightTextLineVisible=Btrue
EditorRightTextLimitLineWidth=I4                             # slightly wider
ColorsText=C-1118482                                         # white
ColorsBackground=C-14474461                                  # carbon
Colors_M_Keywords=C-26368                                    # ambra
Colors_M_Comments=C-10920873                                 # asfalto
Colors_M_Strings=C-6881536                                   # lime
Colors_M_UnterminatedStrings=C-202417                        # yellow
Colors_M_SystemCommands=C-16725605                           # alga
Colors_M_Errors=C-53398                                      # red
Colors_HTML_HTMLLinks=C-6385153                              # violet
Colors_M_Warnings=C-26368                                    # ambra
ColorsMLintAutoFixBackground=C-11184811                      # 
Editor.VariableHighlighting.Color=C-4495617                  # purple
Editor.NonlocalVariableHighlighting.TextColor=C-16725760     # green
Editorhighlight-lines=C-15132391                             # 
Editorhighlight-caret-row-boolean-color=C-16777216           # black
EditorRightTextLimitLineColor=C-13948117                     # 
# XML/HTML
Editor.Language.XML.Color.pi-content=C-6425200
```

### darksteel
```
ColorsUseSystem=Bfalse
ColorsUseMLintAutoFixBackground=Btrue
Editor.VariableHighlighting.Automatic=Btrue
Editor.NonlocalVariableHighlighting=Btrue
EditorCodepadHighVisible=Btrue
EditorCodeBlockDividers=Btrue
Editorhighlight-caret-row-boolean=Btrue
EditorRightTextLineVisible=Btrue
EditorRightTextLimitLineWidth=I1
ColorsText=C-1
ColorsBackground=C-15066598
Colors_M_Keywords=C-1208813
Colors_M_Comments=C-14114579
Colors_M_Strings=C-16724992
Colors_M_UnterminatedStrings=C-4210944
Colors_M_SystemCommands=C-7123493
Colors_M_Errors=C-45747
Colors_HTML_HTMLLinks=C-10592257
Colors_M_Warnings=C-27648
ColorsMLintAutoFixBackground=C-9223357
Editor.VariableHighlighting.Color=C-11184786
Editor.NonlocalVariableHighlighting.TextColor=C-16735351
Editorhighlight-lines=C-14408662
Editorhighlight-caret-row-boolean-color=C-12632257
EditorRightTextLimitLineColor=C-5723992
# TLC
Editor.Language.TLC.Color.Colors_M_Keywords=C-16735351
# C/C++
Editor.Language.C.Color.preprocessor=C-16735351
# VHDL
Editor.Language.VHDL.Color.operator=C-16735351
# Verilog
Editor.Language.Verilog.Color.operator=C-16735351
# XML
Editor.Language.XML.Color.operator=C-1710454
Editor.Language.XML.Color.doctype=C-6578958
Editor.Language.XML.Color.pi-content=C-9868801
```

### monokai
```
ColorsUseSystem=Bfalse
ColorsUseMLintAutoFixBackground=Btrue
Editor.VariableHighlighting.Automatic=Btrue
Editor.NonlocalVariableHighlighting=Btrue
EditorCodepadHighVisible=Btrue
EditorCodeBlockDividers=Btrue
Editorhighlight-caret-row-boolean=Bfalse
EditorRightTextLineVisible=Btrue
EditorRightTextLimitLineWidth=I1
ColorsText=C-460560
ColorsBackground=C-14211038
Colors_M_Keywords=C-448910
Colors_M_Comments=C-9080482
Colors_M_Strings=C-1647756
Colors_M_UnterminatedStrings=C-65536
Colors_M_SystemCommands=C-16711936
Colors_M_Errors=C-65536
Colors_HTML_HTMLLinks=C-16711681
Colors_M_Warnings=C-27648
ColorsMLintAutoFixBackground=C-11974594
Editor.VariableHighlighting.Color=C-10066330
Editor.NonlocalVariableHighlighting.TextColor=C-16729641
Editorhighlight-lines=C-13421773
Editorhighlight-caret-row-boolean-color=C-10066330
EditorRightTextLimitLineColor=C-3355444
Color_CmdWinWarnings=C-26368
```

参考github效果：
https://github.com/scottclowe/matlab-schemer/tree/master/schemes