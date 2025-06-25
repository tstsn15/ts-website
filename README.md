<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>人性的弱点 - 电子书阅读器</title>
    <style>
        /* 基础样式 */
        :root {
            --bg-color: #ffffff;
            --text-color: #333333;
            --primary-color: #4a6baf;
            --secondary-color: #f5f5f5;
            --border-color: #e0e0e0;
            --highlight-color: #f0f7ff;
        }

        .dark-mode {
            --bg-color: #1a1a1a;
            --text-color: #e0e0e0;
            --secondary-color: #2a2a2a;
            --border-color: #444444;
            --highlight-color: #2a3a4a;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: "Segoe UI", "PingFang SC", "Microsoft YaHei", sans-serif;
            background-color: var(--bg-color);
            color: var(--text-color);
            line-height: 1.6;
            transition: all 0.3s ease;
        }

        /* 布局 */
        .container {
            display: grid;
            grid-template-columns: 250px 1fr;
            min-height: 100vh;
        }

        /* 侧边栏 */
        .sidebar {
            background-color: var(--secondary-color);
            padding: 20px;
            border-right: 1px solid var(--border-color);
            overflow-y: auto;
            height: 100vh;
            position: sticky;
            top: 0;
        }

        .book-cover {
            text-align: center;
            margin-bottom: 20px;
        }

        .book-cover img {
            max-width: 100%;
            height: auto;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }

        .book-info h1 {
            font-size: 1.5rem;
            margin-bottom: 10px;
            color: var(--primary-color);
        }

        .book-info .author {
            font-size: 0.9rem;
            color: #666;
            margin-bottom: 15px;
        }

        .book-info .summary {
            font-size: 0.9rem;
            margin-bottom: 20px;
        }

        .controls {
            margin-bottom: 20px;
        }

        .btn {
            display: block;
            width: 100%;
            padding: 8px;
            margin-bottom: 10px;
            background-color: var(--primary-color);
            color: white;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            transition: background-color 0.2s;
        }

        .btn:hover {
            background-color: #3a5a9f;
        }

        .font-controls {
            display: flex;
            justify-content: space-between;
            margin-bottom: 15px;
        }

        .font-controls button {
            flex: 1;
            margin: 0 2px;
        }

        .bookmark-btn {
            background-color: #e67e22;
        }

        .bookmark-btn:hover {
            background-color: #d35400;
        }

        /* 目录 */
        .toc {
            margin-top: 20px;
        }

        .toc h2 {
            font-size: 1.2rem;
            margin-bottom: 15px;
            padding-bottom: 5px;
            border-bottom: 1px solid var(--border-color);
        }

        .toc ul {
            list-style: none;
        }

        .toc li {
            margin-bottom: 8px;
        }

        .toc a {
            display: block;
            padding: 6px 10px;
            color: var(--text-color);
            text-decoration: none;
            border-radius: 4px;
            transition: all 0.2s;
        }

        .toc a:hover {
            background-color: var(--primary-color);
            color: white;
        }

        .toc a.active {
            background-color: var(--primary-color);
            color: white;
        }

        /* 主内容区 */
        .content {
            padding: 30px;
            overflow-y: auto;
            height: 100vh;
        }

        .chapter {
            display: none;
            max-width: 800px;
            margin: 0 auto;
        }

        .chapter.active {
            display: block;
        }

        .chapter h2 {
            font-size: 1.8rem;
            margin-bottom: 20px;
            color: var(--primary-color);
            padding-bottom: 10px;
            border-bottom: 1px solid var(--border-color);
        }

        .chapter h3 {
            font-size: 1.4rem;
            margin: 25px 0 15px;
            color: var(--primary-color);
        }

        .chapter p {
            margin-bottom: 15px;
            text-align: justify;
        }

        .highlight {
            background-color: var(--highlight-color);
        }

        /* 响应式设计 */
        @media (max-width: 768px) {
            .container {
                grid-template-columns: 1fr;
            }

            .sidebar {
                height: auto;
                position: static;
                border-right: none;
                border-bottom: 1px solid var(--border-color);
            }

            .content {
                height: auto;
                padding: 20px;
            }
        }

        /* 打印样式 */
        @media print {
            .sidebar, .controls {
                display: none;
            }

            .content {
                width: 100%;
                height: auto;
                padding: 0;
            }

            .chapter {
                display: block !important;
                page-break-after: always;
            }

            .chapter:last-child {
                page-break-after: avoid;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- 侧边栏 -->
        <aside class="sidebar">
            <div class="book-cover">
                <img src="https://img9.doubanio.com/view/subject/s/public/s1076371.jpg" alt="人性的弱点封面">
            </div>
            <div class="book-info">
                <h1>人性的弱点</h1>
                <div class="author">戴尔·卡耐基 (Dale Carnegie)</div>
                <div class="summary">
                    《人性的弱点》是戴尔·卡耐基的经典作品，汇集了卡耐基的思想精华和最激动人心的内容，成为人类出版史上最畅销的书籍之一。
                </div>
            </div>
            
            <div class="controls">
                <button id="darkModeBtn" class="btn">夜间模式</button>
                <div class="font-controls">
                    <button id="fontDecrease" class="btn">A-</button>
                    <button id="fontReset" class="btn">A</button>
                    <button id="fontIncrease" class="btn">A+</button>
                </div>
                <button id="bookmarkBtn" class="btn bookmark-btn">添加书签</button>
            </div>
            
            <nav class="toc">
                <h2>目录</h2>
                <ul id="tocList">
                    <li><a href="#intro" class="toc-link active">简介</a></li>
                    <li><a href="#chapter1" class="toc-link">第一章 基本技巧</a></li>
                    <li><a href="#chapter2" class="toc-link">第二章 六种使人喜欢您的方法</a></li>
                    <li><a href="#chapter3" class="toc-link">第三章 如何让人赞同您</a></li>
                    <li><a href="#chapter4" class="toc-link">第四章 成为领导者的方法</a></li>
                    <li><a href="#chapter5" class="toc-link">第五章 解决忧虑的基本原则</a></li>
                    <li><a href="#chapter6" class="toc-link">第六章 分析忧虑的方法</a></li>
                    <li><a href="#epilogue" class="toc-link">后记</a></li>
                </ul>
            </nav>
        </aside>
        
        <!-- 主要内容 -->
        <main class="content">
            <!-- 简介 -->
            <div id="intro" class="chapter active">
                <h2>简介</h2>
                <p>《人性的弱点》（How to Win Friends and Influence People）是戴尔·卡耐基的经典著作，自1937年首次出版以来，已被翻译成58种语言，全球销量超过3000万册。</p>
                
                <h3>书籍背景</h3>
                <p>戴尔·卡耐基生于1888年11月24日，是美国著名的人际关系学大师，西方现代人际关系教育的奠基人。他在各种工作经历中发现，一个人在社会上的成功，技术知识只占15%，而人际交往能力则占了85%。</p>
                
                <h3>核心思想</h3>
                <p>本书通过日常生活中常见的案例，系统总结了与人相处的基本技巧、让人喜欢你、赢得他人赞同、成为领导者、解决忧虑等方面的实用方法。书中的原则不仅仅是社交技巧，更是一种生活哲学。</p>
                
                <h3>适用人群</h3>
                <p>无论是商界人士、普通职员、学生还是家庭主妇，都能从本书中获益。它能帮助你:</p>
                <ul>
                    <li>与他人建立良好关系</li>
                    <li>赢得他人合作</li>
                    <li>影响他人而不引起反感</li>
                    <li>提升领导能力</li>
                    <li>减轻忧虑</li>
                </ul>
                
                <p>阅读本书时，建议不要追求速度，而是要边读边思考，尝试将书中的原则应用到日常生活中。每章后的摘要可以帮助你复习关键点。</p>
            </div>
            
            <!-- 第一章 -->
            <div id="chapter1" class="chapter">
                <h2>第一章 基本技巧</h2>
                
                <h3>1. 不要批评、责怪或抱怨</h3>
                <p>批评不但不会改变事实，反而会招致怨恨。心理学家B.F.斯金纳通过动物实验证明，奖励比惩罚更有效。这个原则同样适用于人类。</p>
                <p>林肯最喜欢的一句话是："你不论断他人，就不会被他人论断。"当我们与人相处时，要记住我们不是与逻辑的动物打交道，而是与情绪的动物打交道。</p>
                
                <h3>2. 真诚地赞赏他人</h3>
                <p>约翰·杜威说，人性最深层的需求是"渴望被重视"。赞赏不同于奉承，前者发自内心，后者出自唇齿。前者无私，后者自私。</p>
                <p>查尔斯·施瓦布是美国第一个年薪过百万的管理者。他说："我认为我最宝贵的能力是激发人们热情的能力。我最大的优势是通过赞赏和鼓励充分发挥每个人的潜力。"</p>
                
                <h3>3. 激发他人的强烈需求</h3>
                <p>亨利·福特说："成功的秘诀在于能够站在他人的角度看问题。"如果推销员能向我们展示他们服务如何帮助解决问题，我们就不必被"推销"而会主动购买。</p>
                <p>明天你也许想要劝某人做某事。在你开口前，不妨先问问自己："我怎样才能让这个人自发想要这样做？"这样会让你避免急于求成，而更有效地达成目标。</p>
                
                <div class="chapter-summary">
                    <h3>本章要点：</h3>
                    <ol>
                        <li>不要批评、谴责或抱怨</li>
                        <li>真诚地赞赏他人</li>
                        <li>激发他人的强烈愿望</li>
                    </ol>
                </div>
            </div>
            
            <!-- 第二章 -->
            <div id="chapter2" class="chapter">
                <h2>第二章 六种使人喜欢您的方法</h2>
                
                <h3>1. 真诚地对他人感兴趣</h3>
                <p>如果你想让别人喜欢你，如果你想要发展真正的友谊，如果你想在帮助别人的同时也帮助自己，请记住这个原则：真诚地对他人感兴趣。</p>
                <p>西奥多·罗斯福有个简单但有效的秘诀：他记住每一个仆人的名字，并询问他们家人和生活的情况。这就是为什么他如此受欢迎。</p>
                
                <h3>2. 微笑</h3>
                <p>微笑表示："我喜欢你。你让我快乐。我很高兴见到你。"婴儿的笑容有魔力，狗的热情摇尾会让人快乐。微笑是一种表达方式，超越所有文化障碍。</p>
                <p>纽约一家百货公司的人事经理说，她宁愿雇佣一个小学毕业但总是微笑的女孩，也不愿雇佣一个拥有哲学博士学位但表情忧郁的人。</p>
                
                <h3>3. 记住名字</h3>
                <p>对一个人来说，他的名字是任何语言中最甜美、最重要的声音。记住对方的名字，并在交谈中自然地称呼它，这会赢得对方的好感。</p>
                <p>拿破仑三世曾经自夸，尽管他公务繁忙，他仍然能够记住他所见过的每个人的名字。他的技巧很简单：如果他没听清楚名字，他会请求对方重复；如果是罕见的名字，他会询问如何拼写。</p>
                
                <h3>4. 做一个好的倾听者</h3>
                <p>专注倾听是你能给予他人的最高赞誉。杰克·伍德福德在《陌生爱情》中写道："很少有人能拒绝专心倾听带来的隐含奉承。"</p>
                <p>著名记者艾萨克·马库森采访过许多名人。他说："许多人不能给人留下良好印象，因为他们不专心倾听。他们太关注自己接下来要说什么，结果根本没听对方在说什么。"</p>
                
                <h3>5. 谈论对方感兴趣的事情</h3>
                <p>罗斯福在接待任何访客前，都会熬夜研究客人可能感兴趣的特定主题。因为他知道，通向人心的最佳途径是谈论对他们来说最珍贵的事物。</p>
                <p>与德皇威廉二世交谈时谈论美国，与银行家摩根谈论税收与艺术，与美国劳工领袖戈姆珀斯谈论工人运动，罗斯福总是能找到让对方兴致勃勃的话题。</p>
                
                <h3>6. 使对方感觉重要</h3>
                <p>杜威教授说，人类最深处的渴望是感觉自己重要。想要让人们喜欢你，请让他们感受自己的重要性，并且必须是真诚的。</p>
                <p>记住爱默生的话："我所遇到的每个人在某些方面都比我优秀，因此我可以向他们学习。"承认他人的重要性，并通过真诚的赞赏让他们感受到这一点。</p>
                
                <div class="chapter-summary">
                    <h3>本章要点：</h3>
                    <ol>
                        <li>真诚地对他人感兴趣</li>
                        <li>微笑</li>
                        <li>记住名字</li>
                        <li>做一个好的倾听者</li>
                        <li>谈论对方感兴趣的事情</li>
                        <li>使对方感觉重要</li>
                    </ol>
                </div>
            </div>
            
            <!-- 第三章 -->
            <div id="chapter3" class="chapter">
                <h2>第三章 如何让人赞同您</h2>
                
                <h3>1. 避免争论</h3>
                <p>赢得争论的唯一方法是避免它。争论不可能有赢家，因为你如果输了，当然是输了；而你如果赢了，你还是输了。因为你让对方感到自卑，伤害了他的自尊。</p>
                <p>本杰明·富兰克林说："如果你总是争论、反驳，你也许有时能获胜，但这种胜利是空洞的，因为你永远得不到对方的好感。"</p>
                
                <h3>2. 尊重他人的意见</h3>
                <p>永远不要说"你错了"。直接告诉一个人他错了，相当于对他的判断力、智慧、自尊的一次打击，这只会激起抵抗，而不会想改变他的想法。</p>
                <p>詹姆斯·哈维·罗宾逊在《形成中的心智》中写道："有时我们会发现自己改变想法时毫无抵抗和情绪波动，但如果有人说我们错了，我们就会勃然大怒。"</p>
                
                <h3>3. 如果错了，迅速承认</h3>
                <p>当我们知道自己肯定会被指责时，抢先自己说出来不是更好吗？自我批评比听别人的指责滋味好受得多。</p>
                <p>戴尔·卡耐基曾经有一只叫蒂普的狗不听话到处乱跑，他承认自己没有尽责管理。当他主动道歉并为狗造成的麻烦负责时，邻居们反而开始为他辩护。</p>
                
                <h3>4. 以友善的方式开始</h3>
                <p>"一滴蜂蜜比一加仑胆汁能捉到更多苍蝇。"林肯说。在与人打交道时也是如此。对他人表示友善，可以更容易赢得他们的合作。</p>
                <p>太阳比风更能让人脱下外套。友好和善的态度加上温暖的阳光比严厉的命令和冷风更容易让人改变主意。</p>
                
                <h3>5. 让对方说"是"的开始</h3>
                <p>与人交谈时，不要开始就讨论你们有分歧的地方。先强调并且不断强调你们都认同的事情。让对方一开始就说"是"，而尽量避免他说"不"。</p>
                <p>一个"不"反应是最难克服的心理障碍。当一个人说了"不"，他所有的自尊都要求他保持一致。因此，聪明的说服者会在一开始就引导对方做出肯定回答。</p>
                
                <h3>6. 让对方多说话</h3>
                <p>大多数人试图说服他人时说得太多。让别人把话说出来吧。他们比你更了解自己的事务和问题。问他们问题，让他们告诉你一些事情。</p>
                <p>如果你不同意对方，你也许会想打断他。但不要这样做，这是危险的。当他们急于表达而你不准备好倾听时，他们就不会注意你的观点。</p>
                
                <h3>7. 让别人觉得主意是他自己的</h3>
                <p>没有人喜欢被强行推销或被告知该做什么。我们更喜欢