## copyDataToObject

### 설명
***
* Map의 key값을 이용해 Object의 set함수를 호출하여 Map의 value를 Object에 set해준다.

````java
/*
  import java.util.*;
  import java.lang.reflect.Method;
*/

public static Object copyDataMapToObject(Map<String,Object> map,Object obj){
    String keyAttribute = "";
    String keyAttribute_lower = "";
    String methodString = "";
    Iterator itr = map.keySet().iterator();
    Method[] methods = obj.getClass().getDeclaredMethods();

    while(itr.hasNext()){
        keyAttribute = (String) itr.next();
        methodString = "set" + keyAttribute.substring(0,1).toUpperCase() + keyAttribute.substring(1);
        
        // key값의 대소문자가 불규칙할 경우, object의 property를 모두 소문자로 선언하고, map의 key값도 모두 소문자로 변환하여 진행한다.
        // keyAttribute_lower = keyAttribute.toLowerCase();
        // methodString = "set" + keyAttribute_lower.substring(0, 1).toUpperCase() + keyAttribute_lower.substring(1);
        
        for(int i=0;i<methods.length;i++){
            if(methodString.equals(methods[i].getName())){
                try{
                    methods[i].invoke(obj, map.get(keyAttribute));
                }catch(Exception e){
                    e.printStackTrace();
                }
            }
        }
    }
    return obj;
}
````
