<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>末世互助网</title>
  <style>
    :root {
      --bg: #f5f5f5;
      --text: #111;
      --subtext: #555;
      --border: #ccc;
      --accent: #b30000;
    }

    body {
      background-color: var(--bg);
      color: var(--text);
      font-family: 'Microsoft YaHei', 'PingFang SC', 'Helvetica Neue', Arial, sans-serif;
      margin: 0;
      padding: 0;
      display: flex;
      flex-direction: column;
      align-items: center;
    }

    header {
      width: 100%;
      background-color: #fff;
      border-bottom: 1px solid var(--border);
      text-align: center;
      padding: 15px 0;
    }

    header h1 {
      font-size: 24px;
      margin: 0;
      color: var(--accent);
      letter-spacing: 1px;
    }

    nav {
      width: 100%;
      border-bottom: 1px solid var(--border);
      background: #fff;
      display: flex;
      justify-content: space-around;
      padding: 10px 0;
    }

    nav a {
      color: var(--text);
      text-decoration: none;
      font-weight: 600;
    }

    nav a:hover {
      color: var(--accent);
    }

    #main {
      width: 90%;
      max-width: 1100px;
      padding: 20px;
      margin-top: 15px;
    }

    .card {
      background: white;
      padding: 12px;
      border-radius: 8px;
      box-shadow: 0 1px 4px rgba(0,0,0,0.08);
      margin-bottom: 14px;
    }

    .flex { display:flex; gap:12px; }
    .col { flex:1; }
    input, select, textarea, button { font-size:14px; }
    input, select, textarea { padding:8px; width:100%; box-sizing:border-box; margin-top:6px; margin-bottom:8px; border:1px solid #ddd; border-radius:6px; }
    button { padding:8px 12px; background:#2563eb; color:white; border:0; border-radius:6px; cursor:pointer; }
    button.secondary { background:#6b7280; }
    .small { font-size:12px; color:#666; }
    .muted { color:#666; font-size:13px; }
    ul { padding-left:18px; }
    .tag { display:inline-block; padding:4px 8px; border-radius:12px; background:#eef2ff; margin:4px; font-size:13px; }
    .danger { color:#b91c1c; font-weight:600; }
    .success { color:#065f46; font-weight:600; }
    .inline { display:inline-block; margin-right:8px; }
    .post { border-top:1px dashed #eee; padding:8px 0; }
    .linklike { color:#2563eb; cursor:pointer; text-decoration:underline; }
    .grid-3 { display:grid; grid-template-columns:repeat(3,1fr); gap:8px; }
    .checkbox { display:flex; gap:8px; align-items:center; }
    .stat { display:flex; gap:12px; flex-wrap:wrap; }
    .stat .item { background:#f3f4f6; padding:6px 8px; border-radius:6px; font-size:13px; }
    .tiny { font-size:12px; color:#444; }
    .center { text-align:center; }
    .danger-bg { background:#fff1f2; padding:8px; border-radius:6px; }
    .progress-bar { height: 10px; background: #e5e7eb; border-radius: 5px; overflow: hidden; margin: 5px 0; }
    .progress-fill { height: 100%; }
    .hunger { background: #f59e0b; }
    .fatigue { background: #3b82f6; }
    .san { background: #8b5cf6; }
    .sun { background: #f97316; }
    .period { background: #ec4899; }
    .time-block { display: flex; gap: 10px; margin: 10px 0; }
    .time-option { flex: 1; text-align: center; padding: 8px; border: 1px solid #ddd; border-radius: 6px; cursor: pointer; }
    .time-option.selected { background: #2563eb; color: white; }
    .season-indicator { display: inline-block; padding: 4px 8px; border-radius: 12px; background: #e5e7eb; margin: 0 5px; }
    .weather-indicator { display: inline-block; padding: 4px 8px; border-radius: 12px; background: #dbeafe; margin: 0 5px; }
    .event-card { border-left: 4px solid #b91c1c; padding-left: 10px; margin: 10px 0; }
    .event-good { border-left-color: #065f46; }
    .event-bad { border-left-color: #b91c1c; }
    .admin-badge { background: #b91c1c; color: white; padding: 2px 6px; border-radius: 4px; font-size: 10px; margin-left: 5px; }
  </style>
</head>
<body>
  <header>
    <h1>末世互助网</h1>
    <p style="color: var(--subtext); margin: 5px 0 0;">—— 为仍存活者提供联络与记录 ——</p>
  </header>

  <div id="main">
    <!-- 登入 / 注册（初始） -->
    <div id="authArea" class="card"></div>

    <!-- 主界面 -->
    <div id="appArea" style="display:none;">
      <div class="card flex" id="topBar">
        <div>
          <div class="small">已登录为：<span id="meName"></span> <span class="muted">（<span id="meEmail"></span>）</span><span id="adminBadge" class="admin-badge" style="display:none;">管理员</span></div>
          <div class="tiny">角色：<span id="meCharName"></span> · 性别：<span id="meCharGender"></span> · 年龄：<span id="meCharAge"></span></div>
          <div class="tiny">当前时间：<span id="currentTime"></span> · 季节：<span id="currentSeason"></span> · 天气：<span id="currentWeather"></span></div>
        </div>
        <div style="text-align:right;">
          <div class="small">地点：<span id="meLoc"></span></div>
          <div class="tiny">生存日：<span id="meDays"></span></div>
          <div style="margin-top:6px;">
            <button onclick="nav('home')">主页</button>
            <button onclick="nav('post')">发帖</button>
            <button onclick="nav('monster')">怪物</button>
            <button onclick="nav('resource')">记录/交易</button>
            <button onclick="nav('map')">地图</button>
            <button onclick="nav('profile')">个人</button>
            <button class="secondary" onclick="logout()">登出</button>
          </div>
        </div>
      </div>

      <div id="pages">
        <!-- HOME -->
        <div id="home" class="card page"></div>

        <!-- POST -->
        <div id="post" class="card page" style="display:none;">
          <h3>发表文字帖（纯文本）</h3>
          <textarea id="newPostContent" rows="4" placeholder="写下你在末世的所见、求助、或交易信息..."></textarea>
          <div style="display:flex; gap:8px;">
            <input id="newPostTitle" placeholder="标题（必填）" />
            <input id="newPostLocation" placeholder="地点（可选）" />
            <button onclick="createPost()">发布</button>
          </div>
        </div>

        <!-- MONSTER -->
        <div id="monster" class="card page" style="display:none;">
          <h3>怪物档案（纯文字）</h3>
          <div class="danger-bg">
            <h4>重要提示：被丧尸咬不一定会死</h4>
            <div id="zombieInfo">
              <p><strong>怪物名称：</strong>丧尸</p>
              <p><strong>形成原因：</strong>产生核心在于太阳黑子风暴引发的异常高强度太阳辐射。当活体生物（主要是人类）过度暴露于这种辐射下时，其细胞结构会经历快速崩溃和生物质的异变，最终转化为活性攻击性组织。值得注意的是，被烈日尸咬伤并非导致尸变的主要决定因素。咬伤更主要的危害是传播伤口感染和致命病菌，而非辐射病毒。真正的尸变，几乎总是由直接或间接的辐射过度暴露所引起。</p>
              <p><strong>寿命：</strong>不确定。与季节和光照强度直接挂钩。活跃期（夏季或强光）：它们活动力极强，但细胞代谢和消耗速度也极快。一些个体可能因能量耗尽而快速衰竭，或被高温和辐射加速脱水，最终被"晒成干尸"。休眠期（冬季或阴暗）：缺乏光照和低温会使其活动力大幅下降，并进入类似"冰封"的僵硬状态。理论上，处于这种深度休眠状态的烈日尸可以无限期地存活。</p>
              <p><strong>弱点：</strong></p>
              <ul>
                <li>高强度黑暗与冷却：它们对光照具有依赖性，长时间的黑暗会使其进入迟缓和僵硬状态。突发的极速冷却（如利用冰冻介质）能使其进入假死，易于处理。</li>
                <li>传统中枢破坏：对其脑部或中枢神经系统的传统破坏依然是有效的致命手段。</li>
                <li>辐射屏蔽：特殊合金或厚重结构可以有效隔绝太阳辐射，从而阻止其进一步变异和增强。</li>
              </ul>
              <p><strong>重点注意：</strong></p>
              <ul>
                <li>时间威胁：白天，尤其是夏季正午，是烈日尸攻击力和数量的峰值期。幸存者必须将户外活动降至最低，并将庇护所的防晒和隔热做到极致。</li>
                <li>不一定尸变：由于尸变的核心是辐射而非传染，被咬伤者不会立即变异。同时，人群中可能存在少量对辐射具有免疫或抵抗力的人。</li>
                <li>二次污染：丧尸的血液、体液和残骸可能含有高辐射残留或工业区带来的毒素，接触可能导致中毒或引发二次变异。</li>
              </ul>
            </div>
          </div>
          <div style="margin-top:8px;">
            <input id="newMonsterName" placeholder="怪物名称" />
            <textarea id="newMonsterDesc" placeholder="形成原因" rows="2"></textarea>
            <textarea id="newMonsterLifespan" placeholder="寿命" rows="2"></textarea>
            <textarea id="newMonsterWeakness" placeholder="弱点" rows="2"></textarea>
            <textarea id="newMonsterNotes" placeholder="重点注意" rows="2"></textarea>
            <button onclick="addMonster()">新增怪物</button>
          </div>
          <div id="monsterList" style="margin-top:12px;"></div>
        </div>

        <!-- RESOURCE -->
        <div id="resource" class="card page" style="display:none;">
          <h3>资源记录 / 交易帖（纯文字）</h3>
          <textarea id="newResContent" rows="3" placeholder="资源内容/交易说明，例如：携带 2 罐午餐肉，想在 B镇火车站换 10 升汽油"></textarea>
          <input id="newResLocation" placeholder="地点" />
          <button onclick="createResource()">记录发布</button>
          <div id="resourceList" style="margin-top:12px;"></div>
        </div>

        <!-- MAP -->
        <div id="map" class="card page" style="display:none;">
          <h3>📍 网页涵盖地区地图</h3>
          <p>数据更新时间：末日三年三月一日</p>
          <div style="background:#0b0b0b; color:#dcdcdc; padding:20px; border-radius:6px; text-align:center; font-family:'Courier New', monospace;">
            <p>[地图区域示意图]</p>
            <div style="display:flex; justify-content:center; margin:20px 0;">
              <div style="width:300px; height:200px; background:#333; border:2px solid #555; display:flex; align-items:center; justify-content:center;">
                C市地图
              </div>
            </div>
            <p style="font-size:12px;">A城（历史城区） | C市主城区（核心区） | 高新区/工业区 | B镇（郊区镇）</p>
          </div>
        </div>

        <!-- PROFILE -->
        <div id="profile" class="card page" style="display:none;">
          <h3>角色页面</h3>
          <div class="flex">
            <div class="col">
              <div id="charSummary"></div>
              <div style="margin-top:8px;">
                <h4>时间推进</h4>
                <div class="time-block">
                  <div class="time-option" onclick="selectTimeBlock('morning')">早晨</div>
                  <div class="time-option" onclick="selectTimeBlock('noon')">中午</div>
                  <div class="time-option" onclick="selectTimeBlock('evening')">傍晚</div>
                  <div class="time-option" onclick="selectTimeBlock('night')">夜晚</div>
                </div>
                <div style="margin-top:8px;">
                  <label>本日是否进行"大范围移动"？</label>
                  <select id="movedToday">
                    <option value="0">否（默认）</option>
                    <option value="1">是（+消耗）</option>
                  </select>
                </div>
                <div style="margin-top:8px;">
                  <label>睡眠安排</label>
                  <div style="display:flex; gap:8px;">
                    <select id="sleepAmount">
                      <option value="none">无</option>
                      <option value="half">半 (3小时)</option>
                      <option value="full">整 (6小时)</option>
                    </select>
                    <select id="sleepTime">
                      <option value="morning">早晨</option>
                      <option value="noon">中午</option>
                      <option value="evening">傍晚</option>
                      <option value="night">夜晚</option>
                    </select>
                  </div>
                </div>
                <div style="margin-top:8px;">
                  <button onclick="autoConsume()">自动消耗当日所需</button>
                  <button onclick="advanceTime()">推进时间（处理当前时段）</button>
                  <button class="secondary" onclick="dieNow()">自杀（测试死亡继承）</button>
                </div>
              </div>
              <div id="currentEvent" style="margin-top:12px;"></div>
            </div>
            <div class="col">
              <h4>状态</h4>
              <div id="statusBars"></div>
              <h4 style="margin-top:8px;">背包（上限25）</h4>
              <div id="inventoryList" class="muted tiny"></div>
              <h4 style="margin-top:8px;">Debuffs / 状态</h4>
              <div id="statusList" class="muted tiny"></div>
              <h4 style="margin-top:8px;">来时路（死去角色）</h4>
              <div id="comeFromList" class="muted tiny"></div>
            </div>
          </div>
        </div>

      </div>
    </div>
  </div>

  <footer style="margin-top:30px; padding:10px; text-align:center; color:var(--subtext); font-size:14px; border-top:1px solid var(--border); width:100%;">
    末世互助网 | Version 0.1β | 版权所有 ©2025 Windfall
  </footer>

<script>
/* -------------------------
  数据存储（localStorage）
  key: "ms_user_db" 保存所有用户 {email:{password, profile, char?}}
  每个用户结构示例：
  {
    password: "...",
    nickname: "...",
    email: "...",
    isAdmin: true/false,
    char: { alive:true/false, name, gender, age, profession, buffs:[], debuffs:[], location, envDesc, appearance:[], inventory:{item:count}, daysAlive:0, status:{hunger:0,fatigue:0,sunExposure:0,san:100}, periodCount:0, periodActive:false, comeFrom: [] }
  }
-------------------------*/

/* ---------- 管理员配置（固定内置） ---------- */
const ADMIN_EMAIL = "windfall@ms.local";
const ADMIN_PASS  = "windfall";

// 管理员默认角色模版（用于首次创建管理员用户）
const ADMIN_CHAR_TEMPLATE = {
  alive: true,
  name: "Windfall",
  gender: "其他",
  age: "未知",
  profession: "管理员",
  buffs: [],
  debuffs: [],
  location: "未知",
  envDesc: "管理员专属：系统控制视角",
  appearanceOptions: ["管理员"],
  appearanceChosen: ["管理员"],
  inventory: {}, // 管理员显示为无限资源（特殊处理）
  daysAlive: 0,
  status: { hunger:0, fatigue:0, sunExposure:0, san:100 },
  periodCount: 0,
  periodActive: false,
  comeFrom: []
};

const PROF_LIST = [
  {name: "奶茶店店员", buff: "人际协调：团队关系+10%，减少内讧概率", debuff: "体能偏弱：体力恢复效率 -10%"},
  {name: "心理医生", buff: "精神稳定：san值下降速度 -15%", debuff: "实用性低：医疗类道具使用效果 -10%"},
  {name: "急诊科护士", buff: "急救护理：伤口恢复速度 +20%", debuff: "资源依赖：无药品时医疗效果 -40%"},
  {name: "上班族", buff: "组织规划：物资整理效率 +15%", debuff: "身体僵化：移动速度 -10%"},
  {name: "大学生", buff: "快速学习：学习新技能所需时间 -20%", debuff: "理想主义：初期san值 -10"},
  {name: "游泳教练", buff: "体力好：疲劳值上限 +15", debuff: "专业局限：野外事件成功率 -10%"},
  {name: "程序员", buff: "电路知识：电子类道具修复率 +30%", debuff: "户外经验不足：野外探索事件成功率 -20%"},
  {name: "农民", buff: "农业技能：食物生产量 +20%", debuff: "目光局限：城市事件成功率 -15%"},
  {name: "无业游民", buff: "适应力强：负面事件豁免率 +10%", debuff: "信用低下：团队信任初始 -20"},
  {name: "网红", buff: "表演与说服：外交事件成功率 +20%", debuff: "关注度高：被盯上概率 +15%"},
  {name: "教师", buff: "知识传承：团队经验获取 +10%", debuff: "体力平庸：疲劳消耗 +10%"},
  {name: "开锁师傅", buff: "潜入专家：封闭事件成功率 +25%", debuff: "单打独斗：团队行动协作 -10%"}
];

const LOC_POOL = [
  // A城若干
  "A城·旧街口", "A城·文化街", "A城·老邮局", "A城·豆腐坊",
  // 主城区（C市）
  "C市·行政中心", "C市·商业大道", "C市·地铁口", "C市·高新区边缘",
  // 工业区/郊区 / B镇
  "工业区·仓储厂房", "郊区·菜地边", "B镇·火车站", "B镇·仓库群"
];

const ENV_POOL = [
  "废墟寂静，远处有阵阵金属摩擦声",
  "空气中弥漫焦糊味，天空灰蒙",
  "下着灰色细雨，视线受限",
  "夜幕降临，远处偶有光点",
  "晨雾未散，地面泥泞"
];

// 五大类词库（各选若干供随机挑选）
const AP_FACE = ["吊眼","卧蚕","丹凤眼","桃花眼","下垂眼","单眼皮","双眼皮","浓眉","淡眉","断眉","剑眉","柳眉","塌鼻","鹰鼻","翘鼻","圆鼻","尖下巴","圆下巴","宽额","方额","长脸","鹅蛋脸","眉目疏朗","眉峰凌厉","五官端正"];
const AP_SKIN = ["苍白肤","黝黑肤","古铜肤","麦色肤","冷白肤","黄皮肤","红肤色","青白肤","灰白肤","浅棕肤","深棕肤","肤色通透","肤色晦暗","肤色不均","肤若凝脂","皮肤光洁","肌理细腻","面色红润","面色惨白","面色蜡黄","面色清冷","肤色健康","肤色泛红","肤质粗糙","肤色病态"];
const AP_SCAR = ["刀疤","烧痕","胎记","泪痣","雀斑","酒窝","唇痣","眉心印","鬓角痣","颧侧痣","下巴痣","鼻梁痣","眼下痣","额心疤","唇角裂","眉疤","唇裂","唇钉","耳钉","鼻环","针眼痕","唇角痕","烫痕淡","嘴角印","唇角常裂","额角伤痕"];
const AP_RACE = ["东亚相","南岛相","欧罗面","混血感","亚洲肤","高鼻梁","深眼窝","平颧骨","短面型","立体面","宽脸骨","窄脸骨","颊骨外突","颧高面阔","鼻梁笔直","鼻翼宽阔","额骨平缓","眉弓突出","颧骨低平","下颌坚挺","骨相柔和","骨线分明","面骨深刻","骨感立体","肤骨相衬"];
const AP_IMPRESS = ["眼神凌厉","眼角含笑","眉目紧凑","眉目清朗","五官精致","五官深刻","面容清秀","面目狰狞","面色温柔","神情寡淡","神态倦怠","神色阴沉","神色恍惚","气质冰冷","神情温柔","面容端雅","神态拘谨","表情迟钝","笑容明快","表情冷淡"];

const ITEM_POOL = [
  // 食品
  "压缩饼干","午餐肉罐头","什锦蔬菜罐头","番茄罐头","玉米罐头","牛肉罐头","鸡肉罐头","海鲜罐头","脱水蔬菜","食用盐","糖",
  // 医疗
  "沐浴露","洗发液","洗衣粉","毛巾","家用急救箱","复合维生素","维生素C药片","钙片","胃药","抗生素","退烧止痛药","咳嗽药","止泻药","开塞露","驱蚊花露水","绷带","碘伏","碘酒","创可贴","棉签","电子体温计","卫生巾","肥皂","牙膏","牙刷","塑料袋","卫生纸","暖宝宝","外科手术刀全套",
  // 工具
  "木板","钉子","隔音板","万能胶大管","撬棍","瓦斯罐","防暴钢叉","专业五金工具箱","折叠刀","发电机","指南针","登山绳","登山扣","护目镜","夜视眼镜","多功能救生斧","手摇电筒","基础维修工具","雨伞","雨衣",
  // 燃料与水
  "大桶装矿泉水","小瓶装矿泉水","汽油",
  // 书籍
  "国家地理","无国界医生手册","民兵训练手册","五金手册","法治的细节","演员的自我修养","活着",
  // 防护
  "灭火器","枪","子弹"
];

// 四季定义
const SEASONS = {
  spring: { name: "春季", months: [3,4,5] },
  summer: { name: "夏季", months: [6,7,8] },
  autumn: { name: "秋季", months: [9,10,11] },
  winter: { name: "冬季", months: [12,1,2] }
};

// 天气定义
const WEATHERS = ["晴", "阴", "雨", "风", "雪"];

// 时间定义
const TIME_BLOCKS = {
  morning: { name: "早晨", start: 6, end: 12 },
  noon: { name: "中午", start: 12, end: 14 },
  evening: { name: "傍晚", start: 14, end: 18 },
  night: { name: "夜晚", start: 18, end: 6 }
};

// 初始怪物数据库
let monsterDB = JSON.parse(localStorage.getItem("ms_monsters") || 'null');
if(!monsterDB){ 
  monsterDB = [{
    name: "丧尸", 
    desc: "产生核心在于太阳黑子风暴引发的异常高强度太阳辐射。当活体生物（主要是人类）过度暴露于这种辐射下时，其细胞结构会经历快速崩溃和生物质的异变，最终转化为活性攻击性组织。", 
    lifespan: "不确定。与季节和光照强度直接挂钩。活跃期（夏季或强光）：它们活动力极强，但细胞代谢和消耗速度也极快。一些个体可能因能量耗尽而快速衰竭，或被高温和辐射加速脱水，最终被'晒成干尸'。休眠期（冬季或阴暗）：缺乏光照和低温会使其活动力大幅下降，并进入类似'冰封'的僵硬状态。理论上，处于这种深度休眠状态的烈日尸可以无限期地存活。",
    weakness: "1. 高强度黑暗与冷却：它们对光照具有依赖性，长时间的黑暗会使其进入迟缓和僵硬状态。突发的极速冷却（如利用冰冻介质）能使其进入假死，易于处理。\n2. 传统中枢破坏：对其脑部或中枢神经系统的传统破坏依然是有效的致命手段。\n3. 辐射屏蔽：特殊合金或厚重结构可以有效隔绝太阳辐射，从而阻止其进一步变异和增强。",
    notes: "1. 时间威胁：白天，尤其是夏季正午，是烈日尸攻击力和数量的峰值期。幸存者必须将户外活动降至最低，并将庇护所的防晒和隔热做到极致。\n2. 不一定尸变：由于尸变的核心是辐射而非传染，被咬伤者不会立即变异。同时，人群中可能存在少量对辐射具有免疫或抵抗力的人。\n3. 二次污染：丧尸的血液、体液和残骸可能含有高辐射残留或工业区带来的毒素，接触可能导致中毒或引发二次变异。"
  }]; 
  localStorage.setItem("ms_monsters", JSON.stringify(monsterDB)); 
}

// 事件数据库
const EVENTS = {
  solo: [
    // 环境与辐射威胁
    { type: "bad", text: "A 城：炎热夏季，躲藏在历史建筑的木质阁楼中，因高温和老旧结构，阁楼突然起火或坍塌。" },
    { type: "good", text: "C 市主城区：独自摸索时，发现一栋政府大楼的地下指挥中心，其独立通风和辐射防护系统完好。" },
    { type: "bad", text: "高新区：突发降雨，雨水将高新区的化学废液冲入地下管道，被困者吸入有毒气体。" },
    { type: "bad", text: "B 镇：极寒冬季，藏身在B 镇的金属仓库中，金属外壳快速散热，面临体温过低的风险。" },
    { type: "good", text: "C 市主城区：在环城高架桥下，发现一处天然形成的巨大阴影区域，可在白天低风险停留。" },
    { type: "bad", text: "A 城：在老街区穿行时，被地震余震引发的砖瓦坠落击中，造成内伤。" },
    { type: "bad", text: "工业区：尝试穿越废弃工厂区时，意外触发了残存的工业蒸汽或高压气体泄漏。" },
    { type: "good", text: "B 镇：在 B 镇的农田附近，发现一个尚未被污染的深井，水源稳定且易于提取。" },
    { type: "bad", text: "C 市主城区：潜入地铁站台，发现地下深处的水位正在快速上涨。" },
    { type: "bad", text: "A 城：独自被困于一栋没有窗户的百年老宅中，夏季高温，空气无法流通，几近窒息。" },
    // 生存资源与设备故障
    { type: "good", text: "B 镇：在 B 镇郊区的仓储物流园区，发现一个储存脱水口粮和医疗用品的集装箱。" },
    { type: "bad", text: "A 城：在老城区的狭窄巷道被丧尸围堵，情急之下唯一的防身刀具崩断。" },
    { type: "good", text: "高新区：找到一个被遗弃的太阳能研究机构，获得一套高效且便携的太阳能发电设备。" },
    { type: "bad", text: "C 市主城区：在主干道上，找到一辆油箱充足的汽车，但钥匙在搜寻中意外遗失。" },
    { type: "bad", text: "工业区：找到大量燃料，但装燃料的容器不耐腐蚀，燃料泄漏。" },
    { type: "good", text: "B 镇：在 B 镇的五金厂里，找到制作简易工具和武器所需的大量钢材和焊接设备。" },
    { type: "bad", text: "C 市主城区：唯一的指南针或 GPS 在高楼林立的主城区失灵，迷失方向。" },
    { type: "bad", text: "A 城：发现一处老旧金库，但用来撬锁的工具意外折断，被困在金库外。" },
    { type: "good", text: "高新区：找到一箱军用级夜视仪，让夜间探索变得安全。" },
    { type: "bad", text: "B 镇：独自一人驾车行驶在郊区小道时，轮胎被路面遗留的工业废料刺穿。" },
    // 丧尸与未知生物威胁
    { type: "bad", text: "工业区：遭遇在高温下金属化、皮肤异常坚硬的'工业丧尸'，普通子弹无效。" },
    { type: "bad", text: "C 市主城区：被拥有快速攀爬能力的'高层丧尸'在公寓楼内追击。" },
    { type: "good", text: "A 城：发现 A 城历史城区保留的古老城墙对丧尸具有天然防御效果，可以作为临时庇护所。" },
    { type: "bad", text: "高新区：误入研究机构的试验场地，遭遇具有群体思维的未知生物。" },
    { type: "bad", text: "B 镇：在农田地带，被藏在庄稼地里的晒伤半尸突然袭击，被咬伤。" },
    { type: "good", text: "C 市主城区：找到一个尚未被丧尸发现的地下停车场入口，为逃生提供了一条安全路线。" },
    { type: "bad", text: "A 城：躲藏在老街区的废弃戏院中，被模仿者的哭声引诱，暴露位置。" },
    { type: "bad", text: "工业区：遭遇被有毒化学品感染的丧尸，其血液和体液具有腐蚀性。" },
    { type: "good", text: "B 镇：在 B 镇郊区发现丧尸群正在进行'季节性迁徙'，可趁机潜入。" },
    { type: "bad", text: "C 市主城区：穿越地铁隧道时，遭遇适应黑暗且速度极快的地下变异生物。" },
    // 人性与冲突
    { type: "bad", text: "C 市主城区：远远看到有人在行政中心区抢劫，但对方发现了你，必须立即选择逃跑。" },
    { type: "bad", text: "A 城：遇到一个受伤的陌生人，对方哀求你施救，但你怀疑其是太阳崇拜教的诱饵。" },
    { type: "bad", text: "工业区：在交易中被黑吃黑，对方丢下伪装成物资的工业辐射诱饵后逃跑。" },
    { type: "good", text: "A 城：在老街区的一间古董店中，发现一本详尽的C 市历史地图，标有隐藏通道和地下室。" },
    { type: "bad", text: "B 镇：被一个拥有大型物流车辆的掠夺者团伙发现，独自一人难以抵抗。" },
    { type: "bad", text: "C 市主城区：误入一个被严密武装的幸存者社区，被误认为是间谍而遭到追击。" },
    { type: "good", text: "高新区：发现一个废弃的电台，并成功发出求救信号，收到来自外部城市的简短回复。" },
    { type: "bad", text: "A 城：被人陷害，被误认为是偷盗历史文物的小偷，被其他幸存者追击。" },
    { type: "bad", text: "C 市主城区：发现市中心的金库，但进入需要高风险操作，同时会引来丧尸。" },
    { type: "good", text: "B 镇：在B镇农田发现一个'末世幼儿园'，成功找到一些被救助的孤儿，并得到他们的信任和帮助。" },
    // 特殊事件
    { type: "good", text: "高新区：发现一个废弃的基因实验室，内有丧尸不一定变尸的详细研究资料。" },
    { type: "bad", text: "C 市主城区：唯一的逃生路线（主干道）被一辆装满易燃品的卡车堵死。" },
    { type: "good", text: "A 城：在老城区的中药铺中，找到大量珍贵的传统医疗药材。" },
    { type: "bad", text: "B 镇：在工业园区遭遇突发爆炸，听力或视力受损。" },
    { type: "bad", text: "C 市主城区：发现一个大型商业综合体，但进入后触发了商场的自动卷帘门警报。" },
    { type: "good", text: "高新区：发现一个小型核聚变反应堆模型，虽然无法供电，但其材料可用于制造防辐射盾。" },
    { type: "bad", text: "A 城：找到一座历史悠久的钟楼，但在登顶时楼梯突然坍塌。" },
    { type: "bad", text: "B 镇：唯一的夜视镜被B镇农田的农药或化肥污染，无法使用。" },
    { type: "good", text: "C 市主城区：意外发现一张C 市地下设施的完整工程图。" },
    { type: "bad", text: "工业区：被高新区流出的电子垃圾辐射，导致随身电子设备全部失灵。" }
  ],
  team: [
    // 环境与辐射威胁
    { type: "bad", text: "高新区：团队夏季集体行动，一名队员的防辐射衣在高新区被腐蚀性液体溅到，必须立即处理。" },
    { type: "good", text: "A 城：团队成功清理并占据了 A 城结构最坚固的宗族祠堂作为庇护所。" },
    { type: "bad", text: "B 镇：春季融雪，团队的重型物资车在 B 镇的泥泞农田里抛锚。" },
    { type: "good", text: "C 市主城区：团队成功修复并占据了市政府大楼的紧急供电系统。" },
    { type: "bad", text: "工业区：团队在工业区的大型储油罐附近被困，面临高温和爆炸的双重威胁。" },
    { type: "bad", text: "A 城：团队躲藏在老城区时，被风暴吹倒的百年老树砸中庇护所。" },
    { type: "good", text: "B 镇：团队发现并控制了 B 镇一座废弃的酿酒厂，可用于蒸馏和净化水源。" },
    { type: "bad", text: "C 市主城区：团队在高楼间穿梭时，遭遇突发龙卷风，多人受伤。" },
    { type: "bad", text: "高新区：团队在搜寻中，意外接触到未经处理的核废料，导致全体受到轻微辐射。" },
    { type: "bad", text: "A 城：团队决定在老街区用火取暖，烟雾引来了附近的未知飞行生物。" },
    // 生存资源与设备故障
    { type: "bad", text: "C 市主城区：团队唯一的外科医生在主城区搜寻时，因疏忽从高处坠落重伤。" },
    { type: "bad", text: "B 镇：团队在 B 镇的大型物流中心发现大量物资，但被内部人员私自藏匿。" },
    { type: "good", text: "工业区：团队成功清理并占据了一个废弃的零件加工厂，获得了持续制作武器和工具的能力。" },
    { type: "bad", text: "高新区：团队的所有无线电通讯设备在高新区遭遇电磁脉冲损坏。" },
    { type: "bad", text: "A 城：团队发现一个物资丰富的古董仓库，但内部设置了致命的触发陷阱。" },
    { type: "good", text: "B 镇：团队在 B 镇农田获得了空前的秋季大丰收，确保了未来一年的食物储备。" },
    { type: "bad", text: "C 市主城区：团队集体逃生用的公交车在主干道上，因承重过大而底盘断裂。" },
    { type: "bad", text: "工业区：团队的主发电机在高负荷运转下意外爆炸。" },
    { type: "good", text: "高新区：团队找到一个微型净水系统，只需少量电力即可提供大量纯净饮水。" },
    { type: "bad", text: "A 城：团队成员为了争夺老街区的一块风水宝地作为庇护所，爆发激烈内讧。" },
    // 丧尸与未知生物威胁
    { type: "bad", text: "工业区：团队遭遇'装甲丧尸'：被工业残骸包裹，防御力极高。" },
    { type: "bad", text: "C 市主城区：团队被'不一定尸变'的丧尸咬伤，一名激进队员坚持要对其立即进行'隔离焚烧'。" },
    { type: "good", text: "高新区：团队在生物研究机构找到丧尸的行为分析数据，能精准预测尸群动向。" },
    { type: "bad", text: "A 城：团队躲在古老巷道中，被能够喷吐腐蚀性黏液的未知生物发现。" },
    { type: "bad", text: "B 镇：发现 B 镇郊区的农用无人机被未知生物控制，用于侦查团队位置。" },
    { type: "good", text: "C 市主城区：团队成功截获了一份敌对势力关于安全路线的秘密情报，避开尸群。" },
    { type: "bad", text: "工业区：团队的一名成员被被工业毒素感染的丧尸体液溅到，面临二次感染。" },
    { type: "bad", text: "A 城：团队的孩子或弱小成员在老街区迷路，被潜伏的晒伤半尸抓走。" },
    { type: "good", text: "高新区：团队找到一套完整的防护生化服，可用于在高危区域进行深入搜寻。" },
    { type: "bad", text: "C 市主城区：团队遭遇'尸潮'：丧尸利用主城区密集的交通网络进行大规模移动。" },
    // 人性与冲突
    { type: "bad", text: "C 市主城区：团队与另一个武装团体在行政大楼的资源分配上产生冲突，爆发交火。" },
    { type: "bad", text: "B 镇：团队成员被外部势力以'承诺提供安全农田'为诱饵策反。" },
    { type: "bad", text: "A 城：团队内部因是否要炸毁历史建筑以阻挡尸潮，产生激烈道德争论。" },
    { type: "good", text: "高新区：团队发现并说服一个技术人员小队，通过知识交换建立了长期合作。" },
    { type: "bad", text: "C 市主城区：团队发现一名队员是敌对势力的间谍，故意泄露了撤离路线。" },
    { type: "bad", text: "B 镇：团队遭遇'收割者'：一个专门掠夺 B 镇农作物的团伙。" },
    { type: "good", text: "A 城：团队在老城区建立了一个'中立交易区'，成功吸引周边幸存者进行安全交易。" },
    { type: "bad", text: "工业区：团队发现了一个秘密奴役幸存者的团伙，必须决定是否冒险解救。" },
    { type: "bad", text: "C 市主城区：团队成员为了争夺市政府大楼顶层的通讯设备，导致内讧。" },
    { type: "good", text: "B 镇：团队成功与 B 镇的留守民兵队达成协议，共享防御和情报。" },
    // 特殊事件
    { type: "good", text: "高新区：团队找到一个尚未受损的微型核电站模型，可用于逆向工程以获取能源技术。" },
    { type: "bad", text: "C 市主城区：团队发现地铁线路被敌对势力作为秘密通道，随时可能被偷袭。" },
    { type: "bad", text: "工业区：团队发现丧尸尸变速度与工业辐射水平成正相关。" },
    { type: "good", text: "A 城：团队在老城区的图书馆中，找到大量完好的书籍和地图。" },
    { type: "bad", text: "B 镇：团队的核心医疗物资（如抗辐射药物）在仓储区被动物或丧尸破坏。" },
    { type: "good", text: "高新区：团队成功修复了一个天气监测无人机，能有效进行远程侦查。" },
    { type: "bad", text: "C 市主城区：团队发现所有主要交通要道都被巨型路障彻底封死。" },
    { type: "good", text: "工业区：团队找到一种能有效中和工业区毒素的化学品配方。" },
    { type: "bad", text: "A 城：团队在老街区遭到'反叛者'的袭击，他们利用旧街区的复杂地形进行游击战。" },
    { type: "good", text: "C 市主城区：团队截获了一个来自城市的救援信号，信息中提到了 C 市的一个特定坐标。" }
  ]
};

/* ---------- 帮助函数 ---------- */
function loadDB(){ 
  let db = JSON.parse(localStorage.getItem("ms_user_db") || '{}');
  
  // 检查并创建管理员账户
  if (!db[ADMIN_EMAIL]) {
    db[ADMIN_EMAIL] = {
      password: ADMIN_PASS,
      email: ADMIN_EMAIL,
      nickname: "Windfall",
      isAdmin: true,
      char: ADMIN_CHAR_TEMPLATE
    };
    saveDB(db);
  }
  
  return db;
}
function saveDB(db){ localStorage.setItem("ms_user_db", JSON.stringify(db)); }
function uid(len=8){ return Math.random().toString(36).slice(2,2+len); }
function randChoice(arr){ return arr[Math.floor(Math.random()*arr.length)]; }
function randInt(a,b){ return Math.floor(Math.random()*(b-a+1))+a; }

/* ---------- UI — 登入注册区 ---------- */
function renderAuth(){
  const db = loadDB();
  const html = `
    <h2>登录 / 注册（邮箱+密码）</h2>
    <div style="display:flex; gap:12px;">
      <div style="flex:1;">
        <div class="muted">注册</div>
        <input id="regEmail" placeholder="邮箱" />
        <input id="regPass" placeholder="密码" type="password" />
        <input id="regNick" placeholder="昵称（在末世使用）" />
        <label>性别</label>
        <select id="regGender"><option value="男">男</option><option value="女">女</option><option value="其他">其他</option></select>
        <label>职业</label>
        <select id="regProfession">
          ${PROF_LIST.map(p => `<option value="${p.name}">${p.name}</option>`).join('')}
        </select>
        <button onclick="doRegister()">注册并创建角色</button>
        <div class="small muted">（注册后会生成随机年龄、地点与背包）</div>
      </div>
      <div style="flex:1;">
        <div class="muted">登录</div>
        <input id="logEmail" placeholder="邮箱" />
        <input id="logPass" placeholder="密码" type="password" />
        <button onclick="doLogin()">登录</button>
        <div style="margin-top:8px;">
          <div class="small muted">测试账号：${ADMIN_EMAIL} / ${ADMIN_PASS}</div>
        </div>
      </div>
    </div>
    <hr />
    <div class="small muted">注意：本原型所有数据保存在你本地浏览器的 localStorage；别人无法访问除非你把文件导出或把本项目放到线上。</div>
  `;
  document.getElementById("authArea").innerHTML = html;
}
renderAuth();

/* ---------- 注册与角色生成 ---------- */
function doRegister(){
  const email = document.getElementById("regEmail").value.trim();
  const pass = document.getElementById("regPass").value;
  const nick = document.getElementById("regNick").value.trim() || "匿名幸存者";
  const gender = document.getElementById("regGender").value;
  const profession = document.getElementById("regProfession").value;
  if(!email || !pass){ alert("请填写邮箱和密码"); return; }
  const db = loadDB();
  if(db[email]){ alert("该邮箱已注册，请直接登录"); return; }

  // 生成角色
  const age = randInt(21,35);
  const location = randChoice(LOC_POOL);
  const envDesc = randChoice(ENV_POOL);
  // appearance: 从五类各选2，再随机打乱成10个，玩家后续选3
  const ap = [];
  function pickTwo(arr){ let a=randChoice(arr); let b=randChoice(arr); while(b===a) b=randChoice(arr); return [a,b]; }
  ap.push(...pickTwo(AP_FACE)); ap.push(...pickTwo(AP_SKIN)); ap.push(...pickTwo(AP_SCAR)); ap.push(...pickTwo(AP_RACE)); ap.push(...pickTwo(AP_IMPRESS));
  // 背包：10-20物品，随机挑选并计数
  const inv = {};
  const count = randInt(10,20);
  for(let i=0;i<count;i++){
    const it = randChoice(ITEM_POOL);
    inv[it] = (inv[it]||0)+1;
  }
  // 初始状态
  const char = {
    alive: true,
    name: nick,
    gender,
    age,
    profession,
    buffs: [], debuffs: [],
    location,
    envDesc,
    appearanceOptions: ap, // 10 options
    appearanceChosen: [], // 玩家选3
    inventory: inv,
    daysAlive: 0,
    status: { hunger:0, fatigue:0, sunExposure:0, san:100 }, // 数值用于判断
    periodCount: 0,
    periodActive: false,
    comeFrom: [], // 记录死去角色名
    currentTime: "morning",
    currentSeason: getCurrentSeason(),
    currentWeather: randChoice(WEATHERS),
    consecutiveFatigueDays: 0
  };

  db[email] = { password: pass, email, nickname: nick, char, isAdmin: false };
  saveDB(db);
  alert("注册并生成角色成功！请登录以进入游戏。");
  document.getElementById("regEmail").value=""; document.getElementById("regPass").value=""; document.getElementById("regNick").value="";
}

function doLogin(){
  const email = document.getElementById("logEmail").value.trim();
  const pass = document.getElementById("logPass").value;
  const db = loadDB();
  if(!db[email] || db[email].password !== pass){ alert("邮箱或密码错误"); return; }
  // 登录
  window.currentUser = email;
  showApp();
}

/* ---------- 应用主流程 ---------- */
function showApp(){
  document.getElementById("authArea").style.display='none';
  document.getElementById("appArea").style.display='block';
  updateHeader();
  // Ensure character appearance chosen: if not yet chosen, show selection flow
  const db = loadDB();
  const me = db[window.currentUser];
  if(!me.char) { alert("无角色，请重新注册"); renderAuth(); return; }
  if(me.char.appearanceChosen.length < 3){
    // 展示选择界面让玩家挑3个
    chooseAppearance();
  } else {
    nav('home');
    renderProfile();
    renderMonsters();
    renderHome();
    renderResources();
  }
  updateHeader();
}

function updateHeader(){
  const db = loadDB();
  const me = db[window.currentUser];
  document.getElementById("headerRight").innerHTML = me ? `<span class="muted">欢迎，${me.nickname}</span>` : '';
  
  // 显示管理员徽章
  if (me.isAdmin) {
    document.getElementById("adminBadge").style.display = "inline-block";
  } else {
    document.getElementById("adminBadge").style.display = "none";
  }
}

/* ---------- 外部导航 ---------- */
function nav(page){
  document.querySelectorAll('.page').forEach(p=>p.style.display='none');
  document.getElementById(page).style.display='block';
  if(page==='profile') renderProfile();
  if(page==='monster') renderMonsters();
  if(page==='home') renderHome();
  if(page==='resource') renderResources();
}

/* ---------- 外：选择appearance（第一次登录） ---------- */
function chooseAppearance(){
  const db = loadDB();
  const me = db[window.currentUser];
  const opts = me.char.appearanceOptions; // 10
  let html = `<div><h3>角色外貌 — 从下面 10 项中选择 **3 项** 作为你的角色描述（必须）</h3>`;
  html += `<div class="grid-3">`;
  opts.forEach((o,idx)=> html += `<div class="card tiny"><input type="checkbox" id="ap${idx}" onchange="toggleAp(${idx})" /> <label for="ap${idx}">${o}</label></div>`);
  html += `</div><div style="margin-top:8px;"><button onclick="finishAppearance()">确认（选满3项后即可）</button></div></div>`;
  document.getElementById("authArea").style.display='block';
  document.getElementById("authArea").innerHTML = html;
  document.getElementById("appArea").style.display='none';
  window.tempApChosen = [];
}
function toggleAp(i){
  if(!window.tempApChosen) window.tempApChosen=[];
  const idx = window.tempApChosen.indexOf(i);
  if(idx>=0) window.tempApChosen.splice(idx,1);
  else {
    if(window.tempApChosen.length>=3){ alert("只能选 3 项"); 
      // uncheck last checked visually
      document.getElementById(`ap${i}`).checked=false;
      return; 
    }
    window.tempApChosen.push(i);
  }
}
function finishAppearance(){
  if(!window.tempApChosen || window.tempApChosen.length !==3){ alert("请选 3 项"); return; }
  const db = loadDB(); const me = db[window.currentUser];
  me.char.appearanceChosen = window.tempApChosen.map(i => me.char.appearanceOptions[i]);
  saveDB(db);
  // 回到 app
  document.getElementById("authArea").style.display='none';
  document.getElementById("appArea").style.display='block';
  nav('home');
  renderProfile();
  renderMonsters();
  renderHome();
  renderResources();
}

/* ---------- HOME 帖子与评论 ---------- */
function createPost(){
  const title = document.getElementById("newPostTitle").value.trim();
  const content = document.getElementById("newPostContent").value.trim();
  const loc = document.getElementById("newPostLocation").value.trim();
  if(!title || !content){ alert("请填写标题和内容"); return; }
  const posts = JSON.parse(localStorage.getItem("ms_posts") || '[]');
  const db = loadDB(); const me = db[window.currentUser];
  const post = {
    id: uid(10), author: me.nickname, email: window.currentUser, title, content, loc, time: new Date().toISOString(), comments:[]
  };
  posts.unshift(post);
  localStorage.setItem("ms_posts", JSON.stringify(posts));
  document.getElementById("newPostTitle").value=''; document.getElementById("newPostContent").value='';
  renderHome();
}
function renderHome(){
  const posts = JSON.parse(localStorage.getItem("ms_posts") || '[]');
  let html = `<h3>社区贴子（纯文本）</h3>`;
  html += `<div class="small muted">发布/评论请遵守末世公约（纯文本，无图片）</div>`;
  html += `<div style="margin-top:12px;">`;
  posts.forEach(p=>{
    html += `<div class="post"><strong>${p.title}</strong> <span class="muted">— ${p.author} • ${p.loc||'未知地点'} • ${new Date(p.time).toLocaleString()}</span>`;
    html += `<div style="margin-top:6px;">${escapeHtml(p.content)}</div>`;
    html += `<div style="margin-top:6px;"><span class="linklike" onclick='openComments("${p.id}")'>评论 (${p.comments.length})</span></div>`;
    html += `</div>`;
  });
  html += `</div>`;
  document.getElementById("home").innerHTML = html;
}
function openComments(id){
  const posts = JSON.parse(localStorage.getItem("ms_posts") || '[]');
  const p = posts.find(x=>x.id===id);
  if(!p) return;
  let s = `<h4>${p.title} — 评论</h4><div class="muted">原帖：${escapeHtml(p.content)}</div><div style="margin-top:8px;">`;
  p.comments.forEach(c=> s+=`<div class="card tiny">${c.author}：${escapeHtml(c.text)} <div class="muted small">${new Date(c.time).toLocaleString()}</div></div>`);
  s+=`</div><div style="margin-top:8px;"><input id="replyText" placeholder="写评论..." /> <button onclick='addComment("${p.id}")'>发表评论</button></div>`;
  alertHTML(s);
}
function addComment(postId){
  const text = document.getElementById("replyText").value.trim();
  if(!text){ alert("评论不能为空"); return; }
  const posts = JSON.parse(localStorage.getItem("ms_posts") || '[]');
  const p = posts.find(x=>x.id===postId);
  const db = loadDB(); const me = db[window.currentUser];
  p.comments.push({ author: me.nickname, text, time: new Date().toISOString() });
  localStorage.setItem("ms_posts", JSON.stringify(posts));
  renderHome();
  closeAlertHTML();
}

/* ---------- MONSTER ---------- */
function renderMonsters(){
  monsterDB = JSON.parse(localStorage.getItem("ms_monsters") || '[]');
  let html = `<div>`;
  monsterDB.forEach(m => {
    html += `<div class="card">
      <h4>${m.name}</h4>
      <p><strong>形成原因：</strong>${escapeHtml(m.desc)}</p>
      <p><strong>寿命：</strong>${escapeHtml(m.lifespan)}</p>
      <p><strong>弱点：</strong>${escapeHtml(m.weakness)}</p>
      <p><strong>重点注意：</strong>${escapeHtml(m.notes)}</p>
    </div>`;
  });
  html += `</div>`;
  document.getElementById("monsterList").innerHTML = html;
}
function addMonster(){
  const n = document.getElementById("newMonsterName").value.trim();
  const d = document.getElementById("newMonsterDesc").value.trim();
  const l = document.getElementById("newMonsterLifespan").value.trim();
  const w = document.getElementById("newMonsterWeakness").value.trim();
  const notes = document.getElementById("newMonsterNotes").value.trim();
  if(!n || !d || !l || !w || !notes){ alert("所有字段都要填"); return; }
  monsterDB.push({name:n, desc:d, lifespan:l, weakness:w, notes:notes});
  localStorage.setItem("ms_monsters", JSON.stringify(monsterDB));
  document.getElementById("newMonsterName").value=''; 
  document.getElementById("newMonsterDesc").value='';
  document.getElementById("newMonsterLifespan").value='';
  document.getElementById("newMonsterWeakness").value='';
  document.getElementById("newMonsterNotes").value='';
  renderMonsters();
}

/* ---------- RESOURCE / 交易 ---------- */
function createResource(){
  const content = document.getElementById("newResContent").value.trim();
  const loc = document.getElementById("newResLocation").value.trim();
  if(!content){ alert("请填写内容"); return; }
  const res = JSON.parse(localStorage.getItem("ms_resources") || '[]');
  const db = loadDB(); const me = db[window.currentUser];
  res.unshift({id:uid(8), author:me.nickname, content, loc, time:new Date().toISOString()});
  localStorage.setItem("ms_resources", JSON.stringify(res));
  document.getElementById("newResContent").value=''; document.getElementById("newResLocation").value='';
  renderResources();
}
function renderResources(){
  const res = JSON.parse(localStorage.getItem("ms_resources") || '[]');
  let html = `<h4>资源与交易</h4>`;
  res.forEach(r => {
    html += `<div class="card tiny"><strong>${escapeHtml(r.content)}</strong><div class="muted">${r.author} • ${r.loc||'无地点'} • ${new Date(r.time).toLocaleString()}</div></div>`;
  });
  document.getElementById("resourceList").innerHTML = html;
}

/* ---------- PROFILE / 生存系统 ---------- */
function renderProfile(){
  const db = loadDB(); const me = db[window.currentUser]; const c = me.char;
  document.getElementById("meName").innerText = me.nickname;
  document.getElementById("meEmail").innerText = me.email;
  document.getElementById("meCharName").innerText = c.name;
  document.getElementById("meCharGender").innerText = c.gender;
  document.getElementById("meCharAge").innerText = c.age;
  document.getElementById("meLoc").innerText = c.location + " · " + c.envDesc;
  document.getElementById("meDays").innerText = c.daysAlive;
  document.getElementById("currentTime").innerText = TIME_BLOCKS[c.currentTime].name;
  document.getElementById("currentSeason").innerText = c.currentSeason.name;
  document.getElementById("currentWeather").innerText = c.currentWeather;

  // summary
  let summ = `<div><strong>${c.name}</strong>（${c.gender}）· ${c.age}岁 · 职业：${c.profession}</div>`;
  const prof = PROF_LIST.find(p => p.name === c.profession);
  if (prof) {
    summ += `<div class="muted small">职业特性：${prof.buff}；${prof.debuff}</div>`;
  }
  summ += `<div class="muted small">外貌：${c.appearanceChosen.join('、')}</div>`;
  summ += `<div class="muted small">buffs: ${c.buffs.join(',') || '无'}；debuffs: ${c.debuffs.join(',') || '无'}</div>`;
  summ += `<div style="margin-top:8px;"><strong>当前环境</strong><div class="muted">${c.location} — ${c.envDesc}</div></div>`;
  document.getElementById("charSummary").innerHTML = summ;

  // status bars
  let statusHtml = `
    <div>饥饿值：${c.status.hunger}/100
      <div class="progress-bar"><div class="progress-fill hunger" style="width:${c.status.hunger}%"></div></div>
    </div>
    <div>疲劳值：${c.status.fatigue}/100
      <div class="progress-bar"><div class="progress-fill fatigue" style="width:${c.status.fatigue}%"></div></div>
    </div>
    <div>理智值：${c.status.san}/100
      <div class="progress-bar"><div class="progress-fill san" style="width:${c.status.san}%"></div></div>
    </div>
    <div>阳光暴露：${c.status.sunExposure}/100
      <div class="progress-bar"><div class="progress-fill sun" style="width:${c.status.sunExposure}%"></div></div>
    </div>
  `;
  
  if (c.gender === "女") {
    statusHtml += `
      <div>经期倒数：${c.periodActive ? '进行中' : c.periodCount}/28天
        <div class="progress-bar"><div class="progress-fill period" style="width:${(c.periodActive ? 5 : c.periodCount)/28*100}%"></div></div>
      </div>
    `;
  }
  
  document.getElementById("statusBars").innerHTML = statusHtml;

  // inventory
  let invHtml = '';
  if(me.isAdmin){
    invHtml = '<div style="font-weight:700; color:#b91c1c">无限资源（管理员） ∞</div>';
  } else {
    // 计算背包总物品数
    let totalItems = 0;
    for(const k in c.inventory) totalItems += c.inventory[k];
    
    for(const k in c.inventory) invHtml += `${k} × ${c.inventory[k]}<br/>`;
    invHtml += `<div class="muted">背包使用：${totalItems}/25</div>`;
  }
  document.getElementById("inventoryList").innerHTML = invHtml || '<div class="muted">空</div>';

  // status list
  let st = `饥饿值：${c.status.hunger} / 疲劳值：${c.status.fatigue} / 阳光暴露：${c.status.sunExposure} / 理智值：${c.status.san}`;
  if (c.gender === "女") {
    st += ` / 经期：${c.periodActive ? '进行中' : c.periodCount}/28天`;
  }
  document.getElementById("statusList").innerText = st;

  // comeFrom
  document.getElementById("comeFromList").innerHTML = (c.comeFrom.length? c.comeFrom.map(x=>`<div>${escapeHtml(x)}</div>`).join('') : '<div class="muted">暂无</div>');

  // 选择当前时间段
  document.querySelectorAll('.time-option').forEach(el => {
    el.classList.remove('selected');
    if (el.textContent === TIME_BLOCKS[c.currentTime].name) {
      el.classList.add('selected');
    }
  });
}

// 选择时间段
function selectTimeBlock(time) {
  const db = loadDB(); 
  const me = db[window.currentUser]; 
  const c = me.char;
  c.currentTime = time;
  saveDB(db);
  renderProfile();
}

// 获取当前季节
function getCurrentSeason() {
  const month = new Date().getMonth() + 1; // 1-12
  for (const season in SEASONS) {
    if (SEASONS[season].months.includes(month)) {
      return SEASONS[season];
    }
  }
  return SEASONS.spring; // 默认春季
}

/* 消耗规则与推进时间逻辑 */
function computeConsumables(inv){
  // returns {waterLiters, cansEquivalent}
  let water=0, cans=0;
  for(const k in inv){
    const v = inv[k];
    if(k==="大桶装矿泉水") water += 20 * v;
    else if(k==="小瓶装矿泉水") water += 0.5 * v;
    else if(k.includes("罐头")) cans += 1 * v;
    else if(k==="压缩饼干") cans += 0.25 * v;
    // 其它食品暂不转换为罐头（可拓展）
  }
  return { waterLiters: water, cansEquivalent: cans };
}

function autoConsume(){
  // 尝试从背包中自动扣除当日所需资源（优先用罐头与小瓶水/大桶）
  const db = loadDB(); const me = db[window.currentUser]; const c = me.char;
  if (me.isAdmin) {
    alert("管理员无需消耗资源");
    return;
  }
  
  const moved = document.getElementById("movedToday").value==='1';
  const needCans = moved ? 3 : 2;
  const needWater = 1.5;
  // consume water
  // prefer 小瓶装矿泉水 then 大桶装矿泉水
  function consumeItem(name, num){
    if(c.inventory[name]){
      const take = Math.min(num, c.inventory[name]);
      c.inventory[name] -= take;
      if(c.inventory[name] <=0) delete c.inventory[name];
      return take;
    }
    return 0;
  }
  let gotWater = 0;
  // use small bottles (0.5L each)
  if(c.inventory["小瓶装矿泉水"]) {
    const needBottles = Math.ceil((needWater)/0.5);
    const used = consumeItem("小瓶装矿泉水", needBottles);
    gotWater += used * 0.5;
  }
  if(gotWater < needWater && c.inventory["大桶装矿泉水"]){
    // use barrels as needed
    const needBarrels = Math.ceil((needWater - gotWater) / 20);
    const used = consumeItem("大桶装矿泉水", needBarrels);
    gotWater += used*20;
  }
  // If still short, we fail to fully satisfy water
  // consume cans: prefer full 罐头 then 压缩饼干（0.25罐/个）
  function consumeCans(num){
    let remaining = num;
    // full cans
    const fullCans = Object.keys(c.inventory).filter(k=>k.includes("罐头")).sort();
    for(const k of fullCans){
      if(remaining<=0) break;
      const used = Math.min(c.inventory[k], remaining);
      c.inventory[k] -= used; remaining -= used;
      if(c.inventory[k]<=0) delete c.inventory[k];
    }
    // compressed biscuits
    if(remaining > 0 && c.inventory["压缩饼干"]){
      const neededBiscuits = Math.ceil(remaining / 0.25);
      const used = Math.min(c.inventory["压缩饼干"], neededBiscuits);
      c.inventory["压缩饼干"] -= used;
      const covered = used * 0.25;
      remaining -= covered;
      if(c.inventory["压缩饼干"]<=0) delete c.inventory["压缩饼干"];
    }
    return remaining <= 0;
  }
  const hadCans = computeConsumables(c.inventory).cansEquivalent; // NOTE: uses current inv BEFORE consumption; but we will attempt consume
  const satisfiedFood = consumeCans(needCans);
  // check water satisfied
  const waterAfter = computeConsumables(c.inventory).waterLiters; // actually after consumption; but since we consumed directly using consumeItem, waterAfter is after usage
  const waterSatisfied = (gotWater >= needWater) || (waterAfter >= needWater);
  // Update hunger/fatigue depending on satisfaction
  if(!waterSatisfied || !satisfiedFood){
    // set hunger increase proportionally
    c.status.hunger += (!satisfiedFood?1:0) + (!waterSatisfied?1:0);
  } else {
    // satisfied -> reduce hunger slowly
    c.status.hunger = Math.max(0, c.status.hunger - 1);
  }
  // sleep check not handled here; user sets sleepHrs field and advanceDay will process
  saveDB(db);
  renderProfile();
  alert("尝试自动消耗已执行（若背包资源不足则会造成饥饿）");
}

// 推进时间
function advanceTime() {
  const db = loadDB(); 
  const me = db[window.currentUser]; 
  const c = me.char;
  
  if (me.isAdmin) {
    alert("管理员无需推进时间");
    return;
  }
  
  // 获取用户输入
  const moved = document.getElementById("movedToday").value==='1';
  const sleepAmount = document.getElementById("sleepAmount").value;
  const sleepTime = document.getElementById("sleepTime").value;
  
  // 检查是否在当前时间段睡觉
  const isSleeping = (sleepAmount !== "none" && sleepTime === c.currentTime);
  let sleepHours = 0;
  if (isSleeping) {
    sleepHours = sleepAmount === "half" ? 3 : 6;
  }
  
  // 处理状态变化
  // 每时段饥饿值增加
  c.status.hunger = Math.min(100, c.status.hunger + 10);
  
  // 疲劳值处理
  if (isSleeping) {
    c.status.fatigue = Math.max(0, c.status.fatigue - (sleepHours * 5));
    // 记录连续疲劳天数
    if (sleepHours < 6) {
      c.consecutiveFatigueDays = (c.consecutiveFatigueDays || 0) + 1;
    } else {
      c.consecutiveFatigueDays = 0;
    }
  } else {
    c.status.fatigue = Math.min(100, c.status.fatigue + 10);
    c.consecutiveFatigueDays = (c.consecutiveFatigueDays || 0) + 1;
  }
  
  // 阳光暴露处理（夏季和晴天增加更多）
  if (c.currentSeason.name === "夏季" && c.currentWeather === "晴") {
    c.status.sunExposure = Math.min(100, c.status.sunExposure + 15);
  } else if (c.currentWeather === "晴") {
    c.status.sunExposure = Math.min(100, c.status.sunExposure + 10);
  } else {
    c.status.sunExposure = Math.max(0, c.status.sunExposure - 5);
  }
  
  // 理智值处理
  c.status.san = Math.max(0, c.status.san - 5);
  
  // 女性角色经期处理
  if (c.gender === "女") {
    if (c.periodActive) {
      // 经期进行中，消耗卫生巾
      if (c.inventory["卫生巾"]) {
        c.inventory["卫生巾"] = Math.max(0, c.inventory["卫生巾"] - 1);
        if (c.inventory["卫生巾"] <= 0) delete c.inventory["卫生巾"];
      } else {
        // 没有卫生巾，增加疲劳和降低理智
        c.status.fatigue = Math.min(100, c.status.fatigue + 5);
        c.status.san = Math.max(0, c.status.san - 10);
      }
      
      // 经期持续4-5天
      if (c.periodCount >= 28 + 5) {
        c.periodActive = false;
        c.periodCount = 0;
      } else {
        c.periodCount++;
      }
    } else {
      // 不在经期，增加计数
      c.periodCount++;
      if (c.periodCount >= 28) {
        c.periodActive = true;
      }
    }
    
    // 检查月信紊乱
    if ((c.status.hunger >= 80 || c.status.fatigue >= 80 || c.status.san <= 20) && Math.random() < 0.4) {
      if (!c.debuffs.includes("月信紊乱")) {
        c.debuffs.push("月信紊乱");
        alert("你感到身体不适，出现了月信紊乱的症状。");
      }
    }
    
    // 检查停经
    if (c.debuffs.includes("月信紊乱") && c.debuffs.filter(d => d === "月信紊乱").length >= 3) {
      if (Math.random() < 0.05 && !c.debuffs.includes("停经")) {
        c.debuffs.push("停经");
        c.periodActive = false;
        c.periodCount = 0;
        alert("由于长期的身体不适，你的月经停止了。");
      }
    }
  }
  
  // 处理连续疲劳
  if (c.consecutiveFatigueDays >= 7 && !c.debuffs.includes("疲劳")) {
    c.debuffs.push("疲劳");
    alert("你感到持续的疲劳，难以集中注意力。");
  }
  
  if (c.consecutiveFatigueDays >= 9 && !c.debuffs.includes("眩晕")) {
    c.debuffs.push("眩晕");
    alert("持续的疲劳让你感到头晕目眩，难以察觉周围的危险。");
  }
  
  // 处理 debuffs
  if (c.status.hunger >= 30 && !c.debuffs.includes("饥饿")) c.debuffs.push("饥饿");
  if (c.status.hunger >= 50 && !c.debuffs.includes("虚弱")) c.debuffs.push("虚弱");
  
  if (c.status.fatigue >= 50 && !c.debuffs.includes("疲惫")) c.debuffs.push("疲惫");
  
  if (c.status.san <= 50 && !c.debuffs.includes("焦虑")) c.debuffs.push("焦虑");
  if (c.status.san <= 20 && !c.debuffs.includes("抑郁")) c.debuffs.push("抑郁");
  
  if (c.status.sunExposure >= 50 && !c.debuffs.includes("晒伤")) c.debuffs.push("晒伤");
  if (c.status.sunExposure >= 80 && !c.debuffs.includes("辐射病")) c.debuffs.push("辐射病");
  
  // 检查死亡条件
  if (c.status.hunger >= 100) { doDeath("饿死"); return; }
  if (c.status.fatigue >= 100) { doDeath("猝死"); return; }
  if (c.status.san <= 0) { doDeath("自杀"); return; }
  if (c.status.sunExposure >= 100) { doDeath("阳光灿烂"); return; }
  
  // 随机事件
  const eventPool = EVENTS.solo; // 目前只支持单人事件
  const randomEvent = randChoice(eventPool);
  
  let eventHtml = `<div class="event-card ${randomEvent.type === 'good' ? 'event-good' : 'event-bad'}">`;
  eventHtml += `<strong>${randomEvent.type === 'good' ? '【好事】' : '【坏事】'}</strong> ${randomEvent.text}`;
  eventHtml += `<div style="margin-top:8px;">`;
  eventHtml += `<button onclick="handleEvent('post')">发帖求助</button> `;
  eventHtml += `<button onclick="handleEvent('item')">使用物品</button> `;
  eventHtml += `<button onclick="handleEvent('random')">听天由命</button>`;
  eventHtml += `</div></div>`;
  
  document.getElementById("currentEvent").innerHTML = eventHtml;
  window.currentEvent = randomEvent;
  
  // 移动到下一个时间段
  const timeKeys = Object.keys(TIME_BLOCKS);
  const currentIndex = timeKeys.indexOf(c.currentTime);
  const nextIndex = (currentIndex + 1) % timeKeys.length;
  c.currentTime = timeKeys[nextIndex];
  
  // 如果是新的一天开始
  if (c.currentTime === "morning") {
    c.daysAlive += 1;
    
    // 随机更换天气
    c.currentWeather = randChoice(WEATHERS);
    
    // 每30天更换季节
    if (c.daysAlive % 30 === 0) {
      c.currentSeason = getCurrentSeason();
    }
  }
  
  saveDB(db);
  renderProfile();
}

// 处理事件
function handleEvent(method) {
  const db = loadDB(); 
  const me = db[window.currentUser]; 
  const c = me.char;
  
  let result = "";
  let outcome = "";
  
  switch(method) {
    case 'post':
      result = "你发布了求助帖子，等待其他幸存者的回应。";
      outcome = "pending";
      break;
    case 'item':
      // 检查是否有合适的物品
      const hasSuitableItem = Object.keys(c.inventory).some(item => {
        return isItemSuitableForEvent(item, window.currentEvent);
      });
      
      if (hasSuitableItem) {
        result = "你使用了合适的物品，成功解决了事件。";
        outcome = "success";
        
        // 随机获得道具
        if (Math.random() < 0.3) {
          const newItem = randChoice(ITEM_POOL);
          c.inventory[newItem] = (c.inventory[newItem] || 0) + 1;
          result += ` 并找到了 ${newItem}。`;
        }
      } else {
        result = "你没有合适的物品来处理这个事件。";
        outcome = "failure";
      }
      break;
    case 'random':
      const rand = Math.random();
      if (rand < 0.4) {
        result = "你平安无事地度过了这个事件。";
        outcome = "safe";
      } else if (rand < 0.8) {
        result = "你在事件中受伤了。";
        outcome = "injured";
        
        // 增加疲劳和降低理智
        c.status.fatigue = Math.min(100, c.status.fatigue + 20);
        c.status.san = Math.max(0, c.status.san - 15);
      } else {
        result = "你因祸得福，找到了一些有用的物品。";
        outcome = "lucky";
        
        // 获得随机物品
        const newItem = randChoice(ITEM_POOL);
        c.inventory[newItem] = (c.inventory[newItem] || 0) + 1;
        result += ` 获得了 ${newItem}。`;
      }
      break;
  }
  
  // 根据事件类型调整结果
  if (window.currentEvent.type === 'good' && outcome !== "failure") {
    // 好事通常有更好的结果
    if (outcome === "safe") outcome = "lucky";
    else if (outcome === "injured") outcome = "safe";
  } else if (window.currentEvent.type === 'bad' && outcome !== "success") {
    // 坏事通常有更坏的结果
    if (outcome === "safe") outcome = "injured";
    else if (outcome === "lucky") outcome = "safe";
  }
  
  // 根据最终结果应用效果
  switch(outcome) {
    case "success":
    case "lucky":
      c.status.san = Math.min(100, c.status.san + 10);
      break;
    case "injured":
      c.status.san = Math.max(0, c.status.san - 10);
      break;
    case "failure":
      c.status.san = Math.max(0, c.status.san - 20);
      break;
  }
  
  alert(result);
  document.getElementById("currentEvent").innerHTML = "";
  saveDB(db);
  renderProfile();
}

// 检查物品是否适合事件
function isItemSuitableForEvent(item, event) {
  // 简化的匹配逻辑
  const text = event.text.toLowerCase();
  
  if (text.includes("医疗") || text.includes("受伤") || text.includes("感染")) {
    return item.includes("急救") || item.includes("药") || item.includes("绷带") || item.includes("卫生巾");
  }
  
  if (text.includes("食物") || text.includes("饥饿") || text.includes("罐头")) {
    return item.includes("罐头") || item.includes("饼干") || item.includes("食品");
  }
  
  if (text.includes("水") || text.includes("口渴") || text.includes("脱水")) {
    return item.includes("矿泉水");
  }
  
  if (text.includes("工具") || text.includes("修理") || text.includes("五金")) {
    return item.includes("工具") || item.includes("五金") || item.includes("撬棍");
  }
  
  if (text.includes("武器") || text.includes("防御") || text.includes("攻击")) {
    return item.includes("枪") || item.includes("子弹") || item.includes("斧") || item.includes("刀");
  }
  
  if (text.includes("燃料") || text.includes("汽油") || text.includes("能源")) {
    return item.includes("汽油") || item.includes("发电机");
  }
  
  return false;
}

/* 死亡与继承 */
function doDeath(reason){
  const db = loadDB(); const me = db[window.currentUser]; const c = me.char;
  c.alive = false;
  // 记录来时路
  c.comeFrom.push(`${c.name}（${c.daysAlive}日） - ${reason} @ ${c.location}`);
  // 拿着当前背包作为遗物（新角色继承） —— 这一版本我们把背包留在用户数据中并在创建新角色时复制
  saveDB(db);
  alert(`角色已死亡：${reason}。将返回角色创建界面，新角色会继承死者背包与地点。`);
  // 返回创建界面（保留账号）
  logoutToCreate();
}

function dieNow(){ if(confirm("确定强制令角色死亡以测试继承？")) doDeath("自杀（测试）"); }

/* 注销但不删除账号：登出后回到创建/登录 */
function logout(){
  window.currentUser = null;
  document.getElementById("appArea").style.display='none';
  document.getElementById("authArea").style.display='block';
  renderAuth();
}
function logoutToCreate(){
  // keep logged in but show creation flow: we will create a new character while preserving dead char's inventory as inheritance
  const db = loadDB(); const me = db[window.currentUser];
  // build UI for creating new character that will inherit previous backpack & location
  const prev = me.char;
  let html = `<h3>创建新角色（继承已死角色的背包与地点）</h3>`;
  html += `<div class="muted">你上一个角色 <strong>${prev.name}</strong> 在 ${prev.location} 死亡，背包将被继承。</div>`;
  html += `<input id="newNick" placeholder="新昵称（必填）" />`;
  html += `<label>性别</label><select id="newGender"><option value="男">男</option><option value="女">女</option><option value="其他">其他</option></select>`;
  html += `<label>职业</label><select id="newProfession">
    ${PROF_LIST.map(p => `<option value="${p.name}">${p.name}</option>`).join('')}
  </select>`;
  html += `<div style="margin-top:8px;"><button onclick="createInheritedCharacter()">创建并进入游戏</button></div>`;
  document.getElementById("authArea").innerHTML = html;
  document.getElementById("authArea").style.display='block';
  document.getElementById("appArea").style.display='none';
}

function createInheritedCharacter(){
  const nick = document.getElementById("newNick").value.trim() || "匿名幸存者";
  const gender = document.getElementById("newGender").value;
  const profession = document.getElementById("newProfession").value;
  const db = loadDB(); const me = db[window.currentUser];
  const prev = me.char;
  // create new char but inherit inventory & location & comeFrom
  const age = randInt(21,35);
  const location = prev.location || randChoice(LOC_POOL);
  const envDesc = randChoice(ENV_POOL);
  // appearance options new
  const ap = [];
  function pickTwo(arr){ let a=randChoice(arr); let b=randChoice(arr); while(b===a) b=randChoice(arr); return [a,b]; }
  ap.push(...pickTwo(AP_FACE)); ap.push(...pickTwo(AP_SKIN)); ap.push(...pickTwo(AP_SCAR)); ap.push(...pickTwo(AP_RACE)); ap.push(...pickTwo(AP_IMPRESS));
  // inventory copy
  const inv = JSON.parse(JSON.stringify(prev.inventory || {}));
  const char = {
    alive: true,
    name: nick,
    gender,
    age,
    profession,
    buffs: [], debuffs: [],
    location,
    envDesc,
    appearanceOptions: ap,
    appearanceChosen: [],
    inventory: inv,
    daysAlive: 0,
    status: { hunger:0, fatigue:0, sunExposure:0, san:100 },
    periodCount: 0,
    periodActive: false,
    comeFrom: prev.comeFrom || [],
    currentTime: "morning",
    currentSeason: getCurrentSeason(),
    currentWeather: randChoice(WEATHERS),
    consecutiveFatigueDays: 0
  };
  me.nickname = nick; // update display name
  me.char = char;
  saveDB(db);
  // back to choosing appearance
  window.currentUser = window.currentUser; // keep
  showApp();
}

/* ---------- 工具：安全弹窗与HTML转义 ---------- */
let alertOverlay = null;
function alertHTML(html){
  // create simple modal
  if(alertOverlay) closeAlertHTML();
  alertOverlay = document.createElement('div');
  alertOverlay.style.position='fixed'; alertOverlay.style.left=0; alertOverlay.style.top=0; alertOverlay.style.right=0; alertOverlay.style.bottom=0;
  alertOverlay.style.background='rgba(0,0,0,0.4)'; alertOverlay.style.zIndex=9999; alertOverlay.style.display='flex'; alertOverlay.style.alignItems='center'; alertOverlay.style.justifyContent='center';
  const box = document.createElement('div'); box.style.background='white'; box.style.padding='16px'; box.style.borderRadius='8px'; box.style.maxWidth='700px'; box.style.maxHeight='80%'; box.style.overflow='auto';
  box.innerHTML = html + `<div style="margin-top:8px;text-align:right;"><button onclick="closeAlertHTML()">关闭</button></div>`;
  alertOverlay.appendChild(box);
  document.body.appendChild(alertOverlay);
}
function closeAlertHTML(){ if(alertOverlay){ document.body.removeChild(alertOverlay); alertOverlay=null; } }
function escapeHtml(s){ if(!s) return ''; return s.replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;'); }

/* 启动时检查是否已有登录状态（sessionless: none） */
if(window.currentUser){ showApp(); } else { renderAuth(); }

</script>
</body>
</html>
