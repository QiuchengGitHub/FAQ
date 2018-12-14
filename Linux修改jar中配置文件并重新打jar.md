#修改jar包中的配置文件#
修改jar包中的配置文件

jar包其本质是个zip格式压缩包，加主启动类。

1.	解包至当前目录tmp子目录下 
2.	进入子目录 
3.	修改配置文件 
4.	内部jar文件逐个修改配置：流程相同(解包至tmp子目录、修改配置文件、打包、移除tmp子目录) 
5.	打包至原jar文件 
6.	返回上级目录，删除tmp子目录


		jarfile="test.jar"
		unzip -x "$jarfile" -d "${jarfile}.tmp"  # 解压至临时子目录
		cd "${jarfile}.tmp"
		
		# modify config
		
		zip -ru "../$jarfile" *  # 在临时子目录中更新jar文件
		cd ../
		rm -rf "${jarfile}.tmp
		#test.jar 
		unzip -x test.jar -d test.jar.tmp 
		cd test.jar.tmp 
		vim xxx.properties 
		zip -ru "../test.jar" *