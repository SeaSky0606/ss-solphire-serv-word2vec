#java版word2vector使用说明

```
create by:junhong
date: 2017-02-20
```

- 1 测试用例

````
(comment.txt)
几号 开学 吗
上学 课程 多 吗
学校 有 什么 课程
大学 里面 谈恋爱 了 吗
你 是 怎么 读 大学 的
上 大学 生活 会 有 什么 不 一样
去年 大学 几号 学校 的
单身 生活 与 恋爱 生活 的 区别
````
- 2 模型训练类

```
      public static void main(String[] args) throws IOException {
        Learn learn = new Learn();
        long start = System.currentTimeMillis();
        String path = Learn.class.getClassLoader().getResource("").getPath();
        learn.learnFile(new File(path + "library/comment.txt"));
        System.out.println("use time " + (System.currentTimeMillis() - start));
        learn.saveModel(new File(path + "library/javaVector"));
        System.out.println("-- save done ---");
      }
```
- 3 模型加载与计算类

```
    public static void main(String[] args) throws IOException {

		Word2VEC vec = new Word2VEC();
		String path = Learn.class.getClassLoader().getResource("").getPath();
		vec.loadJavaModel(path + "library/javaVector");

		//System.out.println("wordMap=" + vec.getWordMap());
		String strs[] = {"毛泽东", "你", "的", "吗", "开学", "生活", "恋爱"};
		for (String str : strs) {
			System.out.println(str + "\t" + vec.distance(str));
		}
	}
```
- 4 测试结果

```
result:
毛泽东	
[]
你	
[几号	0.1512225, 区别	0.105051436, 大学	0.07324863, 吗	0.07191756, 读	0.064484626, 有	0.04560892, 什么	0.04451567, ﻿几号	0.044397067, 多	0.0243887, 的	0.01972302, 去年	0.019663095, 会	0.018008891, 单身	0.017954953]
的	
[谈恋爱	0.13655329, 大学	0.09776792, 什么	0.090502314, ﻿几号	0.06358007, 一样	0.05573673, 多	0.053700745, 生活	0.051247604, 去年	0.050584562, 单身	0.04922419]
吗	
[上学	0.19567765, 不	0.16522878, 里面	0.14115049, 恋爱	0.08737221, 学校	0.07880855, 你	0.07191756, 了	0.06601024, 是	0.048410047, 谈恋爱	0.037812416, 一样	0.024150448, 会	0.01976991, 区别	0.011833065, 开学	0.011146497, 有	0.008242807, ﻿几号	0.0029128734]
开学
[里面	0.11983235, 课程	0.08265669, 什么	0.061957378, 谈恋爱	0.057773333, 大学	0.053003673, 上	0.050531298, 是	0.046775483, 读	0.039584536, 的	0.03136791]
生活	
[课程	0.101053946, 学校	0.079275474, 里面	0.07428617, 几号	0.06859991, ﻿几号	0.058182783]
恋爱	
[与	0.21828501, 大学	0.10180222, 吗	0.08737221, 几号	0.076356836, 去年	0.06965362, 怎么	0.057869464, 了	0.04668614, 生活	0.04389965, 一样	0.040114805, 是	0.026322635]

```

###关于文件编码
```
若乱码导致模型训练失败，可查看具体是文件编码还是IDE编码导致！
打印模型具体的'wordMap'即知道模型是否乱码 ‘System.out.println("wordMap=" + vec.getWordMap());’