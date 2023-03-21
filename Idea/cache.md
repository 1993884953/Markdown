```c++
groovyScript("                           
             def result =\"${_1}\";        
             if(result=='byte' ||result=='shot'||result=='int' ||result=='long'||result=='double' ||result=='float'||result=='char'||result=='boolean'||result=='null'||result=='void'){                                                result = result;                                       }else{                                                result =' {@link '+ result + '} ' ;                                        };           return result=='null'||result=='void' ? ' * \\r\\n': ' * @return ' + result +' \\r\\n';              
             " , methodReturnType());
```

```c++
groovyScript("               def result='';               def link='';               def params=\"${_1}\".replaceAll('[\\\\[|\\\\]|\\\\s]','').split(',').toList();  def paramTypes=\"${_2}\".replaceAll('[\\\\[|\\\\]|\\\\s]', '').split(',').toList(); for(i = 0; i < params.size(); i++) {                     if(params[0]==''){break;};                     link=paramTypes[i].split('<').toList()[0];                     result+=' * @param '                         + params[i];                         if(paramTypes[i]=='byte' ||paramTypes[i]=='shot'||paramTypes[i]=='int' ||paramTypes[i]=='long'||paramTypes[i]=='double' ||paramTypes[i]=='float'||paramTypes[i]=='char'||paramTypes[i]=='boolean'){                               result += (' '+link);                         }else{                               result+=' {@link '+ link + '} ' ;                         };                    result+= ((i < params.size() - 1) ? '\\r\\n' : '');              };                 return result == ''||link == 'null' ? null :( result     +'\\r\\n' ) ", methodParameters(), methodParameterTypes())  
```

### 一、线索市场认领线索(普通案例)

线索提供端 :

​	提供普通线索

管理端: 

​	审核通过线索-上架线索

教授端:

​	线索市场认领线索-创建案例-选择合作教授



## 二、教授自己创建案例(需求案例)

教授端:

​	创建案例:

​	是否需要系统匹配线索  **不需要则直接跳到共同点**

管理端:

​	公开案例到线索提交端

线索提交端:

​	教授的需求提供线索

教授端:

​	从待匹配线索的案例下选择认领线索



### 共同点(待匹配研究员及之后)

管理端:

​	是否公开案例到研究员端

​	研究员端申请成为研究员

​	管理端修改人员

教授端:

​	撰写案例

​	案例完成可以更新案例(添加新版本)

管理端选择发表平台

```
{
  申请认领:'/applyForClaim';
  线索市场:'/clueMarket',
  创建项目:"/createProjuct",


  我的案例:{
    开发中的案例:"/casesUnderDevelopment",
    已完成案例:"/completedCases",
    收藏的案例:"/favoriteCases",

  }
  案例市场:"/caseMarket",
  案例管理:{
    线索列表:"/clueList",
    案例需求:"/clueDemand",
    案例列表:"/caseList",

  }
  日志管理:{
    操作日志:"/operationLog",
    登录日志:"/loginLog",

  }
  提供的线索:"/cluesProvided",
  教授的需求:"/Faculty",
  权限管理:{
    用户管理:"/userManagement",
    角色管理:"/roleManagement"
  }

}
```

