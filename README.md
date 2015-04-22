build.xml

<project name="BukkitSamplePlugin" default="dist" basedir=".">
	<property name="pluginname" value="BukkitSamplePlugin"/>
	<property name="bukkit.jar" location="../Bukkit/dist/Bukkit.jar"/>
	<property name="plugins" location="../../plugins/"/>

	<property name="src" location="src"/>
	<property name="bin" location="bin"/>
	<property name="dist" location="dist"/>

	<target name="init">
		<mkdir dir="${bin}"/>
	</target>

	<target name="compile" depends="init">
		<javac srcdir="${src}/main/java" destdir="${bin}" includeantruntime="false">
			<classpath>
				<pathelement location="${bukkit.jar}"/>
			</classpath>
		</javac>
	</target>

	<target name="dist" depends="compile">
		<mkdir dir="${dist}"/>
		<jar jarfile="${dist}/${pluginname}.jar">
			<fileset dir="${bin}"/>
			<fileset file="${src}/main/resources/plugin.yml"/>
		</jar>
	</target>

	<target name="deploy" depends="dist">
		<copy file="${dist}/${pluginname}.jar" todir="${plugins}"/>
	</target>

	<target name="clean">
		<delete dir="${bin}"/>
		<delete dir="${dist}"/>
	</target>
</project>
