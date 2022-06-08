# apex_IG_hide_columns
Oracle APEX Interactive Grid hide column using Javascript

- Create interactive grid using following query and set Static ID "empgrid" to the Interactive Grid Region:
	```plsql
	select ROWID,
		   EMPNO,
		   ENAME,
		   JOB,
		   MGR,
		   HIREDATE,
		   SAL,
		   COMM,
			DEPTNO       
	  from EBA_DEMO_IG_EMP;
	  ```
	  ![](https://github.com/mahmoodsufyan/apex_IG_hide_columns/blob/main/images/1.JPG?raw=true)

- Create list of value item  "P2_JOB":  
	![](https://github.com/mahmoodsufyan/apex_IG_hide_columns/blob/main/images/list_job_item.JPG?raw=true)

- Create dynamic action on change "P2_JOB" item and execute following script.:  
	  ![](https://github.com/mahmoodsufyan/apex_IG_hide_columns/blob/main/images/CREATE_DYNAMIC_ACTION.JPG?raw=true)
		```javascript
		 hideColmIG("empgrid");
		```
- Copy and paste following javascript Function "" to page properties in Function and Global Variable Declaration :
![](https://github.com/mahmoodsufyan/apex_IG_hide_columns/blob/main/images/COPY_JAVASCRIT_FUNCTION.JPG?raw=true)
    ```javascript
     function hideColmIG(pIGStaticID) {
       apex.debug.info("hide colmnig when condition job");
        var grid$ = apex.region(pIGStaticID).call("getCurrentView").view$;
        apex.debug.info(grid$);
        if($v("P2_JOB")== 'MANAGER'){
            grid$.grid("showColumn","COMM");
            grid$.grid("showColumn","SAL");
        } else {
            grid$.grid("hideColumn","COMM");
            grid$.grid("hideColumn","SAL");
        }
        grid$.grid("refreshColumns").grid("refresh");
        apex.debug.info("END hide column");
      }
    ```
    ![](https://github.com/mahmoodsufyan/apex_IG_hide_columns/blob/main/images/PAGE_IG_HIDE_COLUN.JPG?raw=true)
  