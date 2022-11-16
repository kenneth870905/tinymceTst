<template>
    <div>
        <button @click="getContent()">获取内容</button>
		<button @click="addimg()">添加图片</button>
		<Editor ref="editor" api-key="y0wryxiphozxaj3spgx6ivap7k2t3zyvaqwgrxrgcobdacsh" v-model="content" :initial-value="value" @input="input" @onChange="changeValue" :init="init" />
	</div>
</template>
<script>
// import tinymce from "tinymce";
import Editor from "@tinymce/tinymce-vue";
export default {
    name: "TinyMce",
    props: { value: { type: String, value: "" } },
    model: { prop: "value", event: "change" },
    components: {
		Editor
    },
    data() {
        return {
            content: "",
            URL: '',
            init: {
                selector: '#tinydemo2',
                //skin:'oxide-dark',
                // language: 'zh_CN',
                // language: 'zh_CN',
				statusbar: false,
                // plugins : '',
				menu: {
					file: {title: '文件', items: ''},
					edit: {title: '编辑', items: ''},
					// insert: {title: '插入', items: 'link media | template hr'},
					view: {title: '查看', items: ''},
					format: {title: '格式', items: ''},
					table: {title: '表格', items: ''},
					tools: {title: '工具', items: ''}
				},
				plugins:"code",
                plugins: 'code  table charmap hr pagebreak nonbreaking anchor insertdatetime advlist lists wordcount imagetools textpattern help emoticons autosave autoresize',
                toolbar: 'meeting code undo redo restoredraft | cut copy paste pastetext | forecolor backcolor bold italic underline strikethrough link anchor | alignleft aligncenter alignright alignjustify outdent indent | \
    styleselect formatselect fontselect fontsizeselect | bullist numlist | blockquote subscript superscript removeformat | \
    table image media charmap emoticons hr pagebreak insertdatetime print preview | fullscreen | bdmap indent2em lineheight formatpainter axupimgs',
                height: 650, //编辑器高度
                min_height: 400,
                /*content_css: [ //可设置编辑区内容展示的css，谨慎使用
                    '/static/reset.css',
                    '/static/ax.css',
                    '/static/css.css',
                ],*/
                // fontsize_formats: '12px 14px 16px 18px 24px 36px 48px 56px 72px',
                // font_formats: '微软雅黑=Microsoft YaHei,Helvetica Neue,PingFang SC,sans-serif;苹果苹方=PingFang SC,Microsoft YaHei,sans-serif;宋体=simsun,serif;仿宋体=FangSong,serif;黑体=SimHei,sans-serif;Arial=arial,helvetica,sans-serif;Arial Black=arial black,avant garde;Book Antiqua=book antiqua,palatino;',
                // link_list: [
                //     { title: '预置链接1', value: 'http://www.tinymce.com' },
                //     { title: '预置链接2', value: 'http://tinymce.ax-z.cn' }
                // ],
                // image_list: [
                //     { title: '预置图片1', value: 'https://www.tiny.cloud/images/glyph-tinymce@2x.png' },
                //     { title: '预置图片2', value: 'https://www.baidu.com/img/bd_logo1.png' }
                // ],
                // image_class_list: [
                //     { title: 'None', value: '' },
                //     { title: 'Some class', value: 'class-name' }
                // ],
                importcss_append: true,
                
                setup: function (editor) {
                    console.log(123)
                    editor.ui.registry.addButton('meeting', {
                        text: '选择图片',
                        onAction: function () {
                            
                        }

                    });
                },
                toolbar_sticky: true,
                autosave_ask_before_unload: false,
            }
        };
    },
    mounted() {
        //tinymce.init() 
		// tinymce.init({
		// 	selector: '#mydiv',
		// 	inline: true
		// });
    },
    created() {
        this.URL = sessionStorage.getItem("CloudnewUrl");
    },
    methods: {
		getContent(){
			console.log(this.$refs.editor)
			console.log(this.$refs.editor.editor)
			console.log(this.$refs.editor.editor.getContent())
			console.log(this.$refs.editor.editor.getContent({ 'format' : 'text'}))

		},
        changeValue(evt) {
            const value = evt.level.content;
			console.log(value)
            this.$emit("change", value.replace(/(<p><br><\/p>){1,}$/g, ""));
        },
		input(evt){
			console.log(evt)
			
			console.log(this.$refs.editor.editor.getContent({ 'format' : 'text'}))
		},
		addimg(){
			let url = 'http://upload-images.jianshu.io/upload_images/5809200-a99419bb94924e6d.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240'
			let img = "<img src='"+url+"'/>"
			this.$refs.editor.editor.insertContent(img)
		}
    }
};
</script>

<style lang="scss" scoped>
::v-deep .tox-notifications-container{
    display: none;
}
</style>
<style lang="scss">
.tox-notifications-container{
    display: none;
}
</style>
