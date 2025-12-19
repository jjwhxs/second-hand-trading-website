### 系统介绍

基于SpringBoot实现的二手交易网站采用前后端一体化的架构方式，前台系统实现了注册/登录、主页、白菜市场、精选市场、二手手机、二手数码、二手图书、搜索、购物车等功能模块，后台系统实现了主页、用户管理、卖家管理、商品管理、分类管理、快递管理等功能模块。

### 技术选型

开发工具：idea2020.3+Webstorm2020.3

运行环境：jdk1.8+maven3.6.3+mysql5.7

服务端技术：springboot+mybatis+fastjson

前端技术：html+css+ajax+jquery+bootstrap

### 成果展示

注册/登录 输入图片说明

前台系统->主页 输入图片说明

前台系统->白菜市场 输入图片说明

前台系统->精选市场 输入图片说明

前台系统->二手手机 输入图片说明

前台系统->二手数码 输入图片说明

前台系统->二手图书 输入图片说明

后台系统->主页 输入图片说明

后台系统->用户管理 输入图片说明

后台系统->卖家管理 输入图片说明

后台系统->分类管理 输入图片说明

后台系统->快递管理 输入图片说明

### 源码展示

@Controller

@RequestMapping("goods")

public class GoodsController {

@Resource

private GoodsService goodsService;

@Resource

private CategoryService categoryService;

@Resource

private SellerService sellerService;

@Resource

private CartService cartService;

@Resource

private CategoryTwoService categoryTwoService;

//商品详情

@GetMapping("detail/{id}")

public String toDetail(@PathVariable Long id, Model model, HttpSession session){

    // 获取用户 ID
    XxUser user = (XxUser) session.getAttribute("user");

    // 购物车
    List<Cart> cartGoods = new ArrayList<>();
    if (user != null){
        cartGoods = cartService.getByUserId(user.getId());
    }
    Double total = 0.0;
    int goodsCount = cartGoods.size();
    if (cartGoods.size() >0){
        for (int i = 0; i< cartGoods.size(); i++){
            total += cartGoods.get(i).getBuyCount() * cartGoods.get(i).getGoodsPrice();
        }
    }
    // 父分类
    List<Category> categories = categoryService.categoryList();

    // 查询所有子分类
    List<CategoryTwo> categoryTwos = categoryTwoService.getAll();


    //商品详情
    Goods goods = goodsService.detail(id);
    Long categoryId = goods.getCategoryId();
    Long sellerId = goods.getSellerId();
    Category category = categoryService.showCategory(categoryId);
    Seller seller = sellerService.seller(sellerId);

    model.addAttribute("goodsId",id);
    model.addAttribute("goodsCount",goodsCount);
    model.addAttribute("cartGoods",cartGoods);
    model.addAttribute("total",total);
    model.addAttribute("categories",categories);
    model.addAttribute("categoryTwos",categoryTwos);
    model.addAttribute("goods",goods);
    model.addAttribute("category",category);
    model.addAttribute("seller",seller);
    return "shop_single";
    
}

}

### 账号地址及其它说明

1、地址说明

前台系统：localhost:8080

后台系统：localhost:8080/admin/home/

2、账号说明

用户：17777777777/12345678

管理员：admin/123456

3、目录结构展示

输入图片说明

4、项目结构展示

输入图片说明

5、运行步骤

1）创建数据库、导入sql脚本

2）修改application.yml中的数据库配置文件，启动服务端

### 获取方式(可远程调试)

访问链接(在浏览器中手动输入下图中的地址)：

输入图片说明

若资源获取失败，可添加happy35596339(vx)或1204901965(qq)进行交流
