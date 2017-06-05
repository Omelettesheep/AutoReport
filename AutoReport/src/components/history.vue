<template>
<div class="container">
    <div class=" col-md-6 col-md-offset-3">
        <div class="panel panel-sea margin-bottom-40">
            <div class="panel-heading">
                <h3 class="panel-title"><span class="glyphicon glyphicon-menu-right"></span>历史版本</h3>
            </div>
            <table class="table table-striped table-hover app_view_history">
                <tbody>
                    <tr v-for="item in tableList.result" class="history_row">
                        <td class="text-center" style="min-width:120px;" >{{item.version}}</td>
                        <td class="text-center" style="min-width:120px;" >{{item.time}}<br>
                        {{item.desc}}
                        </td>
                    </tr>
                    <!-- <tr class="history_show_more">
                        <td class="text-center warning" colspan="3">查看更多</td>
                    </tr> -->
                </tbody>
            </table>
        </div>
    </div>
</div>
    
</template>

<script>
    export default{
        data(){
            return {
                tableList:{}
            }
        },
        created:function(){
            this.$http.get('/api/detail?type=1').then((data)=>{
                this.tableList = data.body.page;     
            })
        }
    }
</script>

<style>
    .margin-bottom-40 {
        margin-bottom: 40px;
    }

    .panel-sea {
        border-color: #1abc9c;
    }

    .panel-sea > .panel-heading {
    background: #1abc9c;
    }

    .panel-heading {
    color: #fff;
    padding: 5px 15px 4px 15px;
    }


    
    h3{
        line-height: 27px;
    }

    .app_view_history td {
    vertical-align: middle !important;
    }

    .display_none{
        display: none;
    }

    .glyphicon-menu-right:before {
        content: "\e258";
        font-size: 14px;
        padding-right: 5px;
    }

</style>