<范范 html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>范范解忧</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: "SimSun", "宋体", serif;
            background: linear-gradient(135deg, #8B4513 0%, #D2B48C 100%);
            background-image: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" width="100" height="100" viewBox="0 0 100 100"><rect width="100" height="100" fill="%238B4513" opacity="0.1"/><path d="M20,20 L80,80 M80,20 L20,80" stroke="%239C661F" stroke-width="2" opacity="0.3"/></svg>');
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            color: #8B0000;
            padding: 20px;
        }
        
        .container {
            background: rgba(255, 248, 225, 0.95);
            border: 8px double #8B0000;
            border-radius: 15px;
            padding: 40px;
            text-align: center;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
            max-width: 600px;
            width: 100%;
            position: relative;
        }
        
        .container::before {
            content: "⚊";
            position: absolute;
            top: -20px;
            left: -20px;
            font-size: 40px;
            background: #8B0000;
            color: #FFF8E1;
            border-radius: 50%;
            width: 60px;
            height: 60px;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        
        .container::after {
            content: "⚋";
            position: absolute;
            bottom: -20px;
            right: -20px;
            font-size: 40px;
            background: #8B0000;
            color: #FFF8E1;
            border-radius: 50%;
            width: 60px;
            height: 60px;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        
        h1 {
            font-size: 2.8em;
            margin-bottom: 30px;
            color: #8B0000;
            text-shadow: 2px 2px 4px rgba(139, 0, 0, 0.3);
            border-bottom: 3px solid #8B0000;
            padding-bottom: 15px;
            font-family: "SimHei", "黑体", sans-serif;
        }
        
        .hexagram-container {
            margin: 30px 0;
            padding: 30px;
            background: rgba(255, 235, 205, 0.7);
            border: 3px solid #CD853F;
            border-radius: 10px;
            position: relative;
        }
        
        .hexagram-name {
            font-size: 4em;
            font-weight: bold;
            color: #8B0000;
            text-shadow: 3px 3px 6px rgba(0, 0, 0, 0.2);
            margin: 20px 0;
            line-height: 1.2;
        }
        
        .hexagram-number {
            font-size: 1.5em;
            color: #A52A2A;
            margin-top: 10px;
        }
        
        .description {
            font-size: 1.3em;
            line-height: 1.6;
            color: #654321;
            margin-top: 25px;
            text-align: left;
            padding: 0 10px;
        }
        
        .yin-yang {
            width: 80px;
            height: 80px;
            background: conic-gradient(#8B0000 0deg 180deg, #FFF8E1 180deg 360deg);
            border-radius: 50%;
            margin: 20px auto;
            position: relative;
            border: 3px solid #8B0000;
        }
        
        .yin-yang::before, .yin-yang::after {
            content: "";
            position: absolute;
            border-radius: 50%;
            width: 30px;
            height: 30px;
            top: 50%;
            transform: translateY(-50%);
        }
        
        .yin-yang::before {
            background: #FFF8E1;
            left: 10px;
            border: 2px solid #8B0000;
        }
        
        .yin-yang::after {
            background: #8B0000;
            right: 10px;
            border: 2px solid #FFF8E1;
        }
        
        .footer {
            margin-top: 30px;
            font-size: 1.1em;
            color: #A52A2A;
            font-style: italic;
        }
        
        @media (max-width: 768px) {
            .container {
                padding: 20px;
                margin: 10px;
            }
            
            h1 {
                font-size: 2.2em;
            }
            
            .hexagram-name {
                font-size: 3em;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>范范解忧</h1>
        <div class="yin-yang"></div>
        <div class="hexagram-container">
            <div class="hexagram-name" id="hexagramDisplay">正在为您卜卦...</div>
            <div class="hexagram-number" id="hexagramNumber"></div>
        </div>
        <div class="description" id="hexagramDescription"></div>
        <div class="footer">抽3次免费解卦➕护符福袋</div>
    </div>

    <script>
        // 易经64卦数据
        const hexagrams = [
            { name: "乾", number: "第一卦", description: "乾为天，刚健中正。象征创造、进取和领导力。" },
            { name: "坤", number: "第二卦", description: "坤为地，柔顺伸展。象征包容、承载和滋养。" },
            { name: "屯", number: "第三卦", description: "水雷屯，起始维艰。象征创业初期的困难与机遇。" },
            { name: "蒙", number: "第四卦", description: "山水蒙，启蒙奋发。象征教育、学习和开启智慧。" },
            { name: "需", number: "第五卦", description: "水天需，守正待机。象征等待时机和耐心准备。" },
            { name: "讼", number: "第六卦", description: "天水讼，慎争戒讼。象征避免冲突，以和为贵。" },
            { name: "师", number: "第七卦", description: "地水师，行险而顺。象征统率众人，师出有名。" },
            { name: "比", number: "第八卦", description: "水地比，诚信团结。象征亲密合作，相互辅助。" },
            { name: "小畜", number: "第九卦", description: "风天小畜，蓄养待进。象征小有积蓄，逐步发展。" },
            { name: "履", number: "第十卦", description: "天泽履，脚踏实地。象征谨慎行事，履行责任。" },
            { name: "泰", number: "第十一卦", description: "地天泰，国泰民安。象征通达顺利，阴阳和合。" },
            { name: "否", number: "第十二卦", description: "天地否，阻塞不通。象征困难时期，等待转机。" },
            { name: "同人", number: "第十三卦", description: "天火同人，上下和同。象征团结合作，众志成城。" },
            { name: "大有", number: "第十四卦", description: "火天大有，顺天依时。象征大获所有，丰收富足。" },
            { name: "谦", number: "第十五卦", description: "地山谦，内高外低。象征谦虚美德，卑以自牧。" },
            { name: "豫", number: "第十六卦", description: "雷地豫，顺时依势。象征愉悦安乐，顺势而为。" },
            { name: "随", number: "第十七卦", description: "泽雷随，随时变通。象征随从时机，灵活应变。" },
            { name: "蛊", number: "第十八卦", description: "山风蛊，振疲起衰。象征整治弊乱，改革创新。" },
            { name: "临", number: "第十九卦", description: "地泽临，教思无穷。象征亲临指导，监督管理。" },
            { name: "观", number: "第二十卦", description: "风地观，观下瞻上。象征观察学习，审时度势。" },
            { name: "噬嗑", number: "第二十一卦", description: "火雷噬嗑，硬物破碎。象征克服障碍，消除阻力。" },
            { name: "贲", number: "第二十二卦", description: "山火贲，饰外扬质。象征文饰美化，注重礼仪。" },
            { name: "剥", number: "第二十三卦", description: "山地剥，顺势而止。象征剥落衰败，保存实力。" },
            { name: "复", number: "第二十四卦", description: "地雷复，寓动于顺。象征循环往复，复兴重建。" },
            { name: "无妄", number: "第二十五卦", description: "天雷无妄，无妄而得。象征不妄为，顺其自然。" },
            { name: "大畜", number: "第二十六卦", description: "山天大畜，止而不止。象征大有积蓄，厚积薄发。" },
            { name: "颐", number: "第二十七卦", description: "山雷颐，纯正以养。象征养生之道，自食其力。" },
            { name: "大过", number: "第二十八卦", description: "泽风大过，非常行动。象征过度时期，非常手段。" },
            { name: "坎", number: "第二十九卦", description: "坎为水，行险用险。象征险陷重重，沉着应对。" },
            { name: "离", number: "第三十卦", description: "离为火，附和依托。象征光明美丽，依附借助。" },
            { name: "咸", number: "第三十一卦", description: "泽山咸，相互感应。象征感情交流，心灵相通。" },
            { name: "恒", number: "第三十二卦", description: "雷风恒，恒心有成。象征持之以恒，稳定发展。" },
            { name: "遁", number: "第三十三卦", description: "天山遁，遁世救世。象征退避隐忍，以待时机。" },
            { name: "大壮", number: "第三十四卦", description: "雷天大壮，壮勿妄动。象征强盛时期，勿用过猛。" },
            { name: "晋", number: "第三十五卦", description: "火地晋，求进发展。象征前进上升，光明在前。" },
            { name: "明夷", number: "第三十六卦", description: "地火明夷，晦而转明。象征黑暗时期，坚守正道。" },
            { name: "家人", number: "第三十七卦", description: "风火家人，家庭和睦。象征家人团结，和谐相处。" },
            { name: "睽", number: "第三十八卦", description: "火泽睽，异中求同。象征求同存异，化解分歧。" },
            { name: "蹇", number: "第三十九卦", description: "水山蹇，险阻在前。象征艰难险阻，谨慎行事。" },
            { name: "解", number: "第四十卦", description: "雷水解，柔道致治。象征解脱困境，化解矛盾。" },
            { name: "损", number: "第四十一卦", description: "山泽损，损益制衡。象征损下益上，把握分寸。" },
            { name: "益", number: "第四十二卦", description: "风雷益，损上益下。象征增益互助，利人利己。" },
            { name: "夬", number: "第四十三卦", description: "泽天夬，决而能和。象征果断决策，清除邪恶。" },
            { name: "姤", number: "第四十四卦", description: "天风姤，天下有风。象征相遇机缘，防微杜渐。" },
            { name: "萃", number: "第四十五卦", description: "泽地萃，荟萃聚集。象征精英荟萃，团结力量。" },
            { name: "升", number: "第四十六卦", description: "地风升，柔顺谦虚。象征上升发展，逐步高升。" },
            { name: "困", number: "第四十七卦", description: "泽水困，困境求通。象征困境中坚守，等待解脱。" },
            { name: "井", number: "第四十八卦", description: "水风井，求贤若渴。象征修养自身，惠及他人。" },
            { name: "革", number: "第四十九卦", description: "泽火革，顺天应人。象征变革创新，除旧布新。" },
            { name: "鼎", number: "第五十卦", description: "火风鼎，鼎力相助。象征稳定巩固，新陈代谢。" },
            { name: "震", number: "第五十一卦", description: "震为雷，临危不乱。象征震动惊醒，处变不惊。" },
            { name: "艮", number: "第五十二卦", description: "艮为山，动静适时。象征适可而止，保持静止。" },
            { name: "渐", number: "第五十三卦", description: "风山渐，渐进蓄德。象征循序渐进，不急于求成。" },
            { name: "归妹", number: "第五十四卦", description: "雷泽归妹，立家兴业。象征婚嫁结合，组建家庭。" },
            { name: "丰", number: "第五十五卦", description: "雷火丰，日中则斜。象征丰盛盛大，持盈保泰。" },
            { name: "旅", number: "第五十六卦", description: "火山旅，依义顺时。象征旅途漂泊，随机应变。" },
            { name: "巽", number: "第五十七卦", description: "巽为风，谦逊受益。象征顺从进入，以柔克刚。" },
            { name: "兑", number: "第五十八卦", description: "兑为泽，刚内柔外。象征喜悦交流，言语沟通。" },
            { name: "涣", number: "第五十九卦", description: "风水涣，拯救涣散。象征消除隔阂，凝聚人心。" },
            { name: "节", number: "第六十卦", description: "水泽节，万物有节。象征节制适度，自我约束。" },
            { name: "中孚", number: "第六十一卦", description: "风泽中孚，诚信立身。象征诚信感化，心悦诚服。" },
            { name: "小过", number: "第六十二卦", description: "雷山小过，行动有度。象征小有过错，及时改正。" },
            { name: "既济", number: "第六十三卦", description: "水火既济，盛极将衰。象征事已完成，防患未然。" },
            { name: "未济", number: "第六十四卦", description: "火水未济，事业未竟。象征未完成态，继续努力。" }
        ];

        // 使用sessionStorage来保持同一会话中的卦象不变
        function getRandomHexagram() {
            const storedHexagramIndex = sessionStorage.getItem('currentHexagramIndex');
            
            if (storedHexagramIndex !== null) {
                // 如果已存在存储的卦象索引，使用该索引
                return parseInt(storedHexagramIndex);
            } else {
                // 否则生成新的随机卦象并存储
                const randomIndex = Math.floor(Math.random() * hexagrams.length);
                sessionStorage.setItem('currentHexagramIndex', randomIndex.toString());
                return randomIndex;
            }
        }

        // 显示随机卦象
        function displayHexagram() {
            const hexagramIndex = getRandomHexagram();
            const hexagram = hexagrams[hexagramIndex];
            
            document.getElementById('hexagramDisplay').textContent = hexagram.name;
            document.getElementById('hexagramNumber').textContent = hexagram.number;
            document.getElementById('hexagramDescription').textContent = hexagram.description;
        }

        // 页面加载时显示卦象
        window.addEventListener('load', displayHexagram);
    </script>
</body>
</html>
