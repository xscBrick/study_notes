# Study_json

[TOC]

## 顺序执行按钮动作

```js
$container = $('.col-md-10');
 $container.find("#vpcgw_backup_btn").unbind().bind('click', function(){
     if(confirm("确认要执行备份操作？")){
         _doSwitch('backup');
     }
     $container.find("#vpcgw_switch_btn").removeClass('disabled');
 });

$container.find("#vpcgw_switch_btn").unbind().bind('click', function(){
    if(confirm("确认要执行升级切换？")){
        _doSwitch('upgrade');
    }
    $container.find("#vpcgw_rollback_btn").removeClass('disabled');
});

$container.find("#vpcgw_rollback_btn").unbind().bind('click', function(){
    if(confirm("确认要执行回滚操作？")){
        _doSwitch('rollback');
    }
});
```

```php
<div id="vpcgw_view" style="display:none;">
    <div id="vpcgw_options" class="raw" style="float: right;">
        <span>升级版本到：</span><input class="vpcgw_version" value="<?php echo $version; ?>" readonly>
        <span>已执行的时间: </span><span id="page-time" style="color:red;font-size:20px">0</span>秒
        <button class="btn btn-backup" id="vpcgw_backup_btn">备份</button>
        <button class="btn btn-primary vpcgw_switch_btn disabled" id="vpcgw_switch_btn">切换</button>
        <button class="btn btn-success vpcgw_rollback_btn disabled" id="vpcgw_rollback_btn">回退</button>
    </div>

    <div style="width: 900px">
        <table class="table table-striped table-hover">
            <thead>
                <th>IP</th>
                <th>主备状态</th>
                <th>会话数</th>
                <th>流量</th>
                <th>包量</th>
                <th>选择</th>
                <th>状态</th>
            </thead>
            <tbody>
            </tbody>
        </table>
    </div>
</div>
```

```php
<?php
?>
<!doctype html>
<html>
<head>
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
    <title>腾讯云 -APOLLO网络运营系统</title>
    <link href="/application/views/assets/bootstrap/css/bootstrap.min.css"
          rel="stylesheet" media="screen" />
    <link href="/application/views/assets/bootstrap/css/index.css"
          rel="stylesheet" media="screen" />
    <link href="/application/views/assets/jquery-ui/jquery-ui.min.css"
          rel="stylesheet" media="screen" />
    <link href="/application/views/assets/css/common.css" rel="stylesheet"
          media="screen" />
    <link href="/application/views/assets/datatables/buttons/css/buttons.jqueryui.min.css" rel="stylesheet"
          media="screen" />
    <link
        href="/application/views/assets/datatables/css/jquery.dataTables.css"
        rel="stylesheet" media="screen">
    <style type="text/css">
        .more_info_link {
            margin-left: 2px;
            margin-right: 2px;
        }

        #loading_icon {
            position: fixed;
            _position: absolute;
            top: 50%;
            left: 50%;
            width: 124px;
            height: 124px;
            overflow: hidden;
            background: url(/application/views/assets/images/loaderc.gif) no-repeat;
            z-index: 7;
            margin: -62px 0 0 -62px;
        }

        .route_check_content {
            margin: 15px;
        }
    </style>
</head>

<body>
<!--头部 -->
<?php echo $this->load->view('common/header','',true)?>
<!-- 路由 -->
<?php echo $this->load->view('common/page_route','',true)?>
<!-- loading动画 -->
<div id="loading_icon" style="display: none"></div>

<div class="container docs-container">
    <div class="row">
        <div class="col-md-2">
            <!--左侧导航 -->
            <?php echo $this->load->view('vpc/left_banner','',true)?>
        </div>
        <div class="col-md-10" role="main" id="content_main">
            <div id="search_toolbar" style="padding-top: 10px; padding-bottom: 10px">
                <h4>VPCGW集群升级</h4>
                <table>
                    <tr>
                        <td><span>地域：</span></td>
                        <td><select class="span2 region_option_class" id="region_select"></select></td>
                    </tr>
                    <tr>
                        <td><span>VPCGW集群VIP：</span></td>
                        <td><textarea id="vpcgw_vip" cols="20" rows="5"></textarea>(多个IP使用换行分隔，最多输入5个VIP)</td>
                    </tr>
                    <tr>
                        <td><span>升级版本：</span></td>
                        <td><input class="vpcgw_version" readonly value="<?php echo $version; ?>"><button class="btn small-t" type="button" id="add_new_vpcgw_version">新版本</button></td>
                    </tr>
                    <tr>
                        <td colspan="2"><button class="btn btn-primary" type="button" id="get_vpcgw_vip_rip" data-loading-text="查询中...">下一步</button>
                        </td>
                    </tr>
                </table>


            </div>

            <div id="vpcgw_view" style="display:none;">
                <div id="vpcgw_options" class="raw" style="float: right;">
                    <span>升级版本到：</span><input class="vpcgw_version" value="<?php echo $version; ?>" readonly>
                    <span>已执行的时间: </span><span id="page-time" style="color:red;font-size:20px">0</span>秒
                    <button class="btn btn-backup" id="vpcgw_backup_btn">备份</button>
                    <button class="btn btn-primary vpcgw_switch_btn disabled" id="vpcgw_switch_btn">切换</button>
                    <button class="btn btn-success vpcgw_rollback_btn disabled" id="vpcgw_rollback_btn">回退</button>
<!--                    <button class="btn btn-primary" type="button" id="tmp_test_flush" data-loading-text="查询中...">测试刷新数据</button>-->
                </div>

                <div style="width: 900px">
                    <table class="table table-striped table-hover">
                        <thead>
                        <th>IP</th>
                        <th>主备状态</th>
                        <th>会话数</th>
                        <th>流量</th>
                        <th>包量</th>
                        <th>选择</th>
                        <th>状态</th>
                        </thead>
                        <tbody>

                        </tbody>
                    </table>
                </div>
            </div>

            <!-- 加新版本 -->
            <div class="modal fade" id="get_vpcgw_new_version_modal">
                <div class="modal-dialog modal-lg" style="width: 300px">
                    <div class="modal-content">
                        <div class="modal-header">
                            <button type="button" class="close" data-dismiss="modal">
                                <span aria-hidden="true">&times;</span><span class="sr-only">Close</span>
                            </button>
                            <h4 class="modal-title">升级新版本</h4>
                        </div>
                        <div class="modal-body">
                            <h5>
                                <input id="get_vpcgw_new_version_input" type="text" size="29" placeholder="请输入版本号">
                                <div style="text-align: right; margin-top: 10px; padding-right: 10px;">
                                    <button class="btn btn-primary" type="button"
                                            id="set_vpcgw_new_version" data-loading-text="更新中...">添加</button>
                                </div>
                            </h5>
                        </div>
                    </div>
                    <!-- /.modal-content -->
                </div>
                <!-- /.modal-dialog -->
            </div>
            <!-- /.modal -->

        </div>
    </div>
</div>
<!--底部 -->
<?php echo $this->load->view('common/footer','',true)?>
<script src="/application/views/assets/js/jquery.min.js"></script>
<script src="/application/views/assets/jquery-ui/jquery-ui.min.js"></script>
<script type="text/javascript"
        src="/application/views/assets/bootstrap/js/bootstrap.min.js"></script>
<script src="/application/views/assets/Highcharts/js/highcharts.js"></script>
<script src="/application/views/assets/Highcharts/js/modules/exporting.js"></script>
<script type="text/javascript" src="/application/views/assets/js/common.js"></script>
<script type="text/javascript" src="/application/views/vpc/js/vpcgw_switch.js"></script>
</body>
</html>

```



