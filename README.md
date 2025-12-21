### 系统介绍

基于SpringBoot实现的二手交易网站采用前后端一体化的架构方式，前台系统实现了注册/登录、主页、白菜市场、精选市场、二手手机、二手数码、二手图书、搜索、购物车等功能模块，后台系统实现了主页、用户管理、卖家管理、商品管理、分类管理、快递管理等功能模块。

### 技术选型

开发工具：idea2020.3+Webstorm2020.3

运行环境：jdk1.8+maven3.6.3+mysql5.7

服务端技术：springboot+mybatis+fastjson

前端技术：html+css+ajax+jquery+bootstrap

### 成果展示

注册/登录
<img width="1920" height="990" alt="注册登录" src="https://github.com/user-attachments/assets/fe51f69a-51f2-4010-95c2-093f3b61c159" />

前台系统->主页
<img width="1920" height="990" alt="前台系统-主页" src="https://github.com/user-attachments/assets/a93564d0-21b6-4183-8ea5-3e24652d31dc" />

前台系统->白菜市场
<img width="1920" height="990" alt="前台系统-白菜市场" src="https://github.com/user-attachments/assets/0e768a04-8653-4f3f-a065-46a20d665d85" />

前台系统->精选市场
<img width="1920" height="990" alt="前台系统-精选市场" src="https://github.com/user-attachments/assets/b7e0f24a-5c90-46c5-b934-50c39dcd6371" />

前台系统->二手手机
<img width="1920" height="990" alt="前台系统-二手手机" src="https://github.com/user-attachments/assets/01f37a3a-9693-4560-85de-cc07db411324" />

前台系统->二手数码
<img width="1920" height="990" alt="前台系统-二手数码" src="https://github.com/user-attachments/assets/8151b3af-8506-4dbd-9808-7786d6fb376c" />

前台系统->二手图书
<img width="1920" height="990" alt="前台系统-二手图书" src="https://github.com/user-attachments/assets/f9054c19-f8c5-4cbd-9c62-fd41d24856ae" />

后台系统->主页
<img width="1920" height="929" alt="后台系统-主页" src="https://github.com/user-attachments/assets/4116372b-1db2-401c-b82f-e256aa375881" />

后台系统->用户管理
<img width="1920" height="926" alt="后台系统-用户管理" src="https://github.com/user-attachments/assets/c4d2afe4-6b14-4021-b761-30c5f050ecf1" />

后台系统->卖家管理
<img width="1920" height="925" alt="后台系统-卖家管理" src="https://github.com/user-attachments/assets/db97ab12-0c9c-47c3-a7ed-1b4067e2a75b" />

后台系统->分类管理
<img width="1920" height="926" alt="后台系统-分类管理" src="https://github.com/user-attachments/assets/40632d96-3485-40df-ad4f-9449e7e80444" />

后台系统->快递管理
<img width="1920" height="925" alt="后台系统-快递管理" src="https://github.com/user-attachments/assets/5dd6ecd6-fa99-472a-8a05-44b7f7117400" />

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

<img width="977" height="179" alt="目录结构展示" src="https://github.com/user-attachments/assets/7dc85824-ab83-45fe-b281-67ebe91fc83e" />

4、项目结构展示

<img width="1729" height="984" alt="项目结构展示" src="https://github.com/user-attachments/assets/5ea71ab1-9d72-4864-a454-44fbffdb9eff" />

5、运行步骤

1）创建数据库、导入sql脚本

2）修改application.yml中的数据库配置文件，启动服务端

### 获取方式(可远程调试)

访问链接(在浏览器中手动输入下图中的地址)：

<img width="1040" height="135" alt="链接" src="https://github.com/user-attachments/assets/642e1c6e-0c5c-4520-b411-b4fa4231be47" />

若资源获取失败，可添加happy35596339(vx)或1204901965(qq)进行交流
