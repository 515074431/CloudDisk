<template>
    <div class="cd-main FileContent">
        <WindowsHeader :data=header style="border-bottom: 2px solid #6ce26c;"></WindowsHeader>
        <div class="FileShowContainer">
            <iframe :src="LoadUrl"></iframe>
        </div>
    </div>
</template>

<script>
    import WindowsHeader from "./DiskWindow/WindowHeader";
    export default {
        name: "DiskFileContent",
        components:{WindowsHeader},
        data(){
            return{
                NowLoad:{
                    disk_name:'',
                    content:''
                },
                LoadUrl:'',
                header:{
                    title:"",
                }
            }
        },
        created(){
            this.$ipc.on('win-data', (event, data)=>{//接收打开文本文件的数据
                this.$nextTick(()=>{
                    this.NowLoad=data;
                    this.header.title=data.disk_name+' 文件查看';
                    this.LoadUrl=this.$path.join(__static, '/syntaxhighlighter/index.html?id=')+data.disk_id+'&type='+data.type;
                });
            });
        }
    }
</script>

<style scoped>
    /*文件查看窗口*/
    .FileShowContainer {
        width: 100%;
        height: calc(100% - 30px);
    }
    .FileShowContainer iframe{
        overflow: auto;
    }
</style>