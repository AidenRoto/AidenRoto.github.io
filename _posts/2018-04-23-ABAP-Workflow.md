---
layout: post
title:  " [SAP/ABAP] Workflow "
subtitle:   " 기본자료"
categories: abap
tags: 
---

# SAP / ABAP 

## 전체적인 흐름

* INCLUDE 로 **_top _scr _f01 _o01 _i01** 을 나누어 코드를 관리한다.
* INITIALIZATION 에서 Company Code 확인 후 권한 확인


```abap
FORM set_initilization .

  data: ls_999 type ZKESMM999.

  CALL FUNCTION 'Z_KEMM00_SEARCH_COMPANYCODE'
    EXPORTING
      i_uname       = sy-uname
   IMPORTING
     GT_999        = ls_999.

  move: ls_999-c_bukrs to p_bukrs.

ENDFORM.                    " SET_INITILIZATION
 ```
* START-OF-SELECTION 순서대로 코드 작성
* 마지막 부분에 call screen 0100. 
  * PBO (process before output)
  * PAI (process after input)

```
MODULE user_command_0100 INPUT.

  MOVE g_okcode TO g_saveok.
  CLEAR g_okcode.

  CASE g_saveok.

    WHEN 'BACK'.
      LEAVE TO SCREEN 0.

    when 'ENTER'.
      message i001 with 'Information'.

    when 'GO_200'.
      call screen 0200.

  ENDCASE.

ENDMODULE.         
```
