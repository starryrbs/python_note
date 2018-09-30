##Python项目-Day35
1. 数组去重

	1. 使用indexof

			for (let item of array){
			        //判断数组中item的位置
			        if (array2.indexOf(item)==-1){
			            array2.push(item);
			        }
			    }


	2. 使用双层循环

			for (let i=0;i<array.length;i++){
			        for (let j=i+1;j<array.length;j++){
			            if (array[i]==array[j]){
			                array.splice(j,1);
			                j--;
			            }
			        }
			    }




2. json

	json的定义:


		user={
		        "username":"aa",
		        "psd":"a"
		    };


	访问json:

		alert(user.psd);

	遍历json:

		for (let key in user){
	        console.log(key);
	        console.log(user[key]);
	    }

3. Math

	Math常用的对象属性

		* E   返回算术常量 e，即自然对数的底数（约等于2.718）。
		* PI  返回圆周率（约等于3.14159）。


	Math对象方法

	
	
