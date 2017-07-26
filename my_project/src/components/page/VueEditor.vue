<template>
    <div>
        <div class="crumbs">
            <el-breadcrumb separator="/">
                <el-breadcrumb-item><i class="el-icon-date"></i> 表单</el-breadcrumb-item>
                <el-breadcrumb-item>编辑器</el-breadcrumb-item>
            </el-breadcrumb>
        </div>
       
        <quill-editor ref="myTextEditor" v-model="content" :config="editorOption"></quill-editor>
        <el-button class="editor-btn" type="primary" @click="submit">提交</el-button>

        <div class="comment">
        	<ul id="list"></ul>
        </div>
    </div>
   	
</template>

<script>
    import { quillEditor } from 'vue-quill-editor';
    export default {
        data: function(){
            return {
                content: '<p>Hello BBK</p>',
                contenteditor:"",
                contentext:"",                
                editorOption: {
                    // something config
                }
            }
        },
        components: {
            quillEditor
        },
        methods: {
            onEditorChange({ editor, html, text }) {
                this.content = html;
            },
            submit(){

                console.log(this.contenteditor)
                console.log(this.contentext)                
                this.$message.success('提交成功！');                
                var li = document.createElement("li");                
                var span = document.createElement("span");                
                var pinglun = document.createElement("p");                
                var huifu = document.createElement("p");    
                huifu.style.color="#333";                     
                huifu.style.display="inline-block";   
                huifu.style.marginTop="5px";   
                huifu.style.marginBottom="5px";                   
                huifu.innerHTML = "<i style='margin-right:15px;'>回复</i>";
                huifu.onclick=function(){
                	var textarea = document.createElement("textarea"); 
                	var i = document.createElement("i");        
                	i.style.color="#0082E6";                	
                	i.style.marginLeft="10px";                	                	
                	i.innerHTML='确定';                	
                	textarea.style.width="300px";
                	textarea.style.height="50px";
					textarea.style.padding="10px";
					textarea.style.marginTop="10px";
										
                	li.appendChild(textarea);
                	li.appendChild(i);                      	
                	i.onclick=function(){
                		var textareacontent = textarea.value;
                		textarea.style.display='none';
                		this.style.display='none';
	                	var odiv = document.createElement("div"); 
						odiv.style.marginLeft="20px";	
						odiv.style.fontSize="10px";
						odiv.innerHTML = textareacontent;
	                	li.appendChild(odiv);
                	}
                }
                span.appendChild(huifu);
                li.style.marginTop="20px";
                li.style.padding="5px";                
                li.innerHTML = "<b>"+this.content+"</b>";                   
                li.appendChild(span);
                document.getElementById("list").appendChild(li);
                this.content='';
                
            }
        },
        computed: {
            editor() {
                return this.$refs.myTextEditor.quillEditor;               
            }
        }
    }
</script>
<style scoped>
    .editor-btn{
        margin-top: 20px;
    }
    .comment{
   		margin-top:10px;
   }
   #list{
   	  	list-style: none;  	  	 	
   }
   
  .comment li{   		
   		margin-top:50px;
   		padding:5px;
   		background: red;
   }
   
  #list li span{
		display: block;  
		width: 100%;
		height: 100%;	
		margin-top: 20px;

  }

</style>