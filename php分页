<html>
<head>
  <meta http-equiv="content-type" content="text/html; charset=utf-8">
</head>
<body>
<?php
/*  重要语句
  echo "<pre>";
  print_r($_SERVER);  */
/* 1传入页码 */
   $page = $_GET['p'];
/* 2根据页码取出数据：php->mysql处理 */
  $host = 'localhost';
  $username = 'root';
  $password = '';
  $db = 'test01';
  $pageSize = 10;//显示条数

//连接数据库
  $conn = mysqli_connect($host, $username, $password);
  if(!$conn){
    echo "数据库连接失败";
    exit;  //终止程序
  }
//选择所要操作的数据库
  mysqli_select_db($conn, $db);
//设置数据库编码格式
  mysqli_query($conn,"set names utf8");
//编写sql获取分页数据SELECT * FROM 表名 LIMIT 起始位置，显示条数
  $sql = "SELECT *  FROM test001 LIMIT " . ($page - 1) * $pageSize . ", {$pageSize}";
//  $sql = "SELECT *  FROM test001";
//把sql语句传送数据中
//  $result = mysqli_query($conn, $sql);
  $result = $conn->query($sql);
//处理我们的数据
  if($result -> num_rows >0){
    echo "<table border=2  cellspacing=0 width=40% bgcolor='aqua'>";
    echo "<tr><td>ID</td> <td>NAME</td></tr>";
    while($row = $result ->fetch_assoc()){
//      printf($row['id'] . '-' . $row['name']  . '<br>');

//      echo $row['id'] . '-' . $row['name']  . '<br>';
      echo '<tr>';
      echo "<td>{$row['id']}</td>";
      echo "<td>{$row['name']}</td>";
      echo '<tr>';
    }
    echo "</table>";
  }else{
    echo "0";
  }
//  释放结果，关闭连接
   mysqli_free_result($result);
//  $conn -> close();
//  获取数据总数
  $total_sql = "SELECT COUNT(*) FROM test001";
  $total_result =mysqli_fetch_array($conn -> query($total_sql));
//  print_r($total_result);
  $total = $total_result[0];
//  echo $total;exit;
  $total_pages = ceil($total/$pageSize);
/** 3显示数据 + 分页条 **/
  $page_banner = "";
  if($page>1){
    $page_banner .= "<a href='" .$_SERVER['PHP_SELF']."?p=1'>首页</a>";
    $page_banner .= "<a href='" .$_SERVER['PHP_SELF']."?p=".($page-1)."'>上一页</a>";
  }
  if($page<$total_pages){
    $page_banner .= "<a href='" .$_SERVER['PHP_SELF']."?p=".($page+1)."'>下一页</a>";
    $page_banner .= "<a href='" .$_SERVER['PHP_SELF']."?p=".($total_pages)."'>尾页</a>";
  }
  $page_banner .= " 共有：{$total_pages}页";
  echo $page_banner;
?>
</body>
</html>
