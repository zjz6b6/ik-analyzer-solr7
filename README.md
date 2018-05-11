# ik-analyzer-solr7
ik-analyzer for solr7.x
<p>IKAnalyzer的作者为林良益（linliangyi2007@gmail.com），项目网站为http://code.google.com/p/ik-analyzer/</p>

<h3>适配最新版solr7，并添加动态加载字典表功能；</h3>
<h3>在不需要重启solr服务的情况下加载新增的字典。</h3>

<hr>
<h2>使用说明：</h2><br>
<pre>
&lt;!-- Maven仓库地址 --&gt;
&lt;dependency&gt;
    &lt;groupId&gt;com.github.magese&lt;/groupId&gt;
    &lt;artifactId&gt;ik-analyzer-solr7&lt;/artifactId&gt;
    &lt;version&gt;7.x&lt;/version&gt;
&lt;/dependency&gt;
</pre>
<ul>
    <li>
        <p>1. 将jar包放入solr服务的jetty或tomcat的webapp/WEB-INF/lib/目录下；</p>
    </li>
    <li>
        <p>2. 将resources目录下的5个配置文件放入solr服务的jetty或tomcat的webapp/WEB-INF/classes/目录下；</p>
<pre>
①IKAnalyzer.cfg.xml
②ext.dic
③stopword.dic
④ik.conf
⑤dynamicdic.txt
</pre>
    </li>
    <li>
        <p>3. 配置solr的managed-schema，添加ik分词器，示例如下；</p>
<pre>
&lt;!-- ik分词器 --&gt;
&lt;fieldType name="text_ik" class="solr.TextField"&gt;
  &lt;analyzer type="index"&gt;
      &lt;tokenizer class="org.wltea.analyzer.lucene.IKTokenizerFactory" useSmart="false" conf="ik.conf"/&gt;
      &lt;filter class="solr.LowerCaseFilterFactory"/&gt;
  &lt;/analyzer&gt;
  &lt;analyzer type="query"&gt;
      &lt;tokenizer class="org.wltea.analyzer.lucene.IKTokenizerFactory" useSmart="true" conf="ik.conf"/&gt;
      &lt;filter class="solr.LowerCaseFilterFactory"/&gt;
  &lt;/analyzer&gt;
&lt;/fieldType&gt;
</pre>
    </li>
    <li>
        <p>4. 启动solr服务测试分词；</p>
    </li>
    <li>
        <p>5. ik.conf文件说明：</p>
<pre>
files=dynamicdic.txt
lastupdate=0
</pre>
        <p>files为动态字典列表，可以设置多个字典表，用逗号进行分隔，默认动态字典表为dynamicdic.txt；</p>
        <p>lastupdate默认值为0，每次对动态字典表修改后请+1，不然不会将字典表中新的词语添加到内存中，lastupdate采用的是int类型，不支持时间戳，如果使用时间戳的朋友可以把源码中的int改成long即可；</p>
    </li>
    <li>
        <p>5-dynamicdic.txt 为动态字典，在此文件配置的词语不需重启服务即可加载进内存中；</p>
    </li>
</ul>
<hr>

<p>有问题可以联系作者邮箱magese@live.cn；</p>
<p>欢迎大家一起交流~</p>
