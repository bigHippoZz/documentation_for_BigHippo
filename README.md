# Vue 3 + Typescript + Vite

This template should help get you started developing with Vue 3 and Typescript in Vite.

## Recommended IDE Setup

[VSCode](https://code.visualstudio.com/) + [Vetur](https://marketplace.visualstudio.com/items?itemName=octref.vetur). Make sure to enable `vetur.experimental.templateInterpolationService` in settings!

### If Using `<script setup>`

[`<script setup>`](https://github.com/vuejs/rfcs/pull/227) is a feature that is currently in RFC stage. To get proper IDE support for the syntax, use [Volar](https://marketplace.visualstudio.com/items?itemName=johnsoncodehk.volar) instead of Vetur (and disable Vetur).

## Type Support For `.vue` Imports in TS

Since TypeScript cannot handle type information for `.vue` imports, they are shimmed to be a generic Vue component type by default. In most cases this is fine if you don't really care about component prop types outside of templates. However, if you wish to get actual prop types in `.vue` imports (for example to get props validation when using manual `h(...)` calls), you can use the following:

### If Using Volar

Run `Volar: Switch TS Plugin on/off` from VSCode command palette.

### If Using Vetur

1. Install and add `@vuedx/typescript-plugin-vue` to the [plugins section](https://www.typescriptlang.org/tsconfig#plugins) in `tsconfig.json`
2. Delete `src/shims-vue.d.ts` as it is no longer needed to provide module info to Typescript
3. Open `src/main.ts` in VSCode
4. Open the VSCode command palette
5. Search and run "Select TypeScript version" -> "Use workspace version"



# 逻辑思维判断

1. 编写程序的时候惯性思维是在开始的地方进行错误判断，这时候基本上都是 if(!stack.length) return false;

2. 写 if()判断的时候 记住一个事情，这是进行写错误判断还是正确判断这是很重要的！！！！
3. 写错误判断的时候，如果出现 condition !== '1 ' condition === '1'
   · condition !== '1' 理解并记住这是排除 `1` 当不是 1 的情况都可以，而且这是错误判断，那么说 除了 1 其他的都是错误情况 -> 条件广泛
   · condition === `1` 理解并记住这是 确定就是 1 当必须是 1 的情况才可以，这是错误判断，说明 1 是错误情况 -> 条件严格
4. 如果出现 if(){} else {} 一定要注意观察两个判断哪个判断能能够少 并且一步到位

# while 循环判断

1. 首先 while 中的判断条件是可以理解为，当这个条件满足的时候会一直执行。
2. 所以这时候进行编写 condition 的时候，一种是先思考其中停止条件然后进行取反，另一种直接思考什么情况他会一直执行，什么情况下他会天停止执行。
3. 基本上可以这样想，先想停止条件然后进行取反。

# 数组的 index 循环索引问题

index < array.length 临界值是 index 正好等于 array.length

### 解题思路 这个的题解已经有 1.1k 了，之前我也一直在总结递归的写法，可以说直到这个题，我才敢以肯定我自己总结的思路，不管这个我解决递归的思路是错是对，都挺愿意能让大家看到。**这个思路对写递归代码来说，还是比较简单适用的，比我看到的这些把递归掰开来揉碎了来讲的要更容易出代码**。希望对写递归还比较迷茫的同学们有所帮助，如果我写的对你有帮助，还望大家能多点赞转发。 ### 先放结论 **Rules Number One**，基本上，**所有的递归问题都可以用递推公式来表示。有了这个递推公式，我们就可以很轻松地将它改为递归代码。**。所以，遇到递归不要怕，先想**递推公式**。 ##### 例 1: (比较明显的能递推公式的问题)

问题：斐波那契数列的第 n 项
递推公式：
f(n)=f(n-1)+f(n-2) 其中，f(0)=0,f(1)=1
终止条件：
if (n <= 2) return 1;
递归代码：
int f(int n) {
if (n <= 2) return 1;
return f(n-1) + f(n-2);
}

##### 例 2:(不那么明显的有递推公式的问题)

问题：逆序打印一个数组
递推公式：
假设令 F(n)=逆序遍历长度为 n 的数组
那么 F(n)= 打印数组中下标为 n 的元素 + F(n-1)
终止条件：
if (n <0) return ;
递归代码：
public void Print(int[] nums,int n){
if(n<0) return;
System.out.println(nums[n]);
Print(nums,n-1);
}
到这里，不知道大家对写递归有没有一些理解了。其实写递归不能总想着去把递归平铺展开，这样脑子里就会循环，一层一层往下调，然后再一层一层返回，试图想搞清楚计算机每一步都是怎么执行的，这样就很容易被绕进去。对于递归代码，这种试图想清楚整个递和归过程的做法，实际上是进入了一个思维误区。只要找到**递推公式**，我们就能很轻松地写出递归代码。

到这里，我想进一步跟大家说明我这个思路是比较能够容易出代码的，那么就树的遍历问题来和大家讲。递归总是和树分不开，其中，最典型的便是树的遍历问题。刚开始学的时候，不知道大家是怎么理解先／中／后序遍历的递归写法的，这里我提供我的思路供参考，以前序遍历为例：

问题：二叉树的先序遍历
递推公式：
令 F(Root)为问题:遍历以 Root 为根节点的二叉树，
令 F(Root.left)为问题:遍历以 F(Root.left)为根节点的二叉树
令 F(Root.right)为问题:遍历以 F(Root.right)为根节点的二叉树
那么其递推公式为：
F(Root)=遍历 Root 节点+F(Root.left)+F(Root.right)
递归代码：
public void preOrder(TreeNode node){
if(node==null) return;
System.out.println(node.val);
preOrder(node.left);
preOrder(node.righr);
}
**Rules Number Two**, **递归是一种关于某个重复动作(完成重复性的功能)的形式化描述**。具体点讲，如果一个问题 A 可以分解为若干子问题 B、C、D，**你可以假设子问题 B、C、D 已经解决，在此基础上思考如何解决问题 A**。而且，你只需要思考问题 A 与子问题 B、C、D 两层之间的关系即可，不需要一层一层往下思考子问题与子子问题，子子问题与子子子问题之间的关系(也就是说，递归只能考虑当前层和下一层的关系，不能继续往下深入)。我们需要屏蔽掉递归细节，理解为完成了某种功能的形式化描述即可。

好了，那我们来分析这个题。

问题：单向链表的反转
递推公式：
令 F(node)为问题:反转以 node 为头节点的单向链表；
一般，我们需要考虑 F(n)和 F(n-1)的关系，那么这里，如果 n 代表以 node 为头节点的单向链表，那么 n-1 就代表以 node.next 为头节点的单向链表.
所以，我们令 F(node.next)为问题：反转以 node.next 为头节点的单向链表；
那么，F(node)和 F(node.next)之间的关系是？这里我们来简单画个图，假设我们反转 3 个节点的链表：
1 -> 2 -> 3
那么，F(node=1)=F(node=2)+?
这里假设子问题 F(node=2)已经解决，那么我们如何解决 F(node=1)：
很明显，我们需要反转 node=2 和 node=1， 即 node.next.next=node; 同时 node.next=null;
所以，这个问题就可以是：F(node=1)=F(node=2)+ 反转 node=2 和 node=1
递归代码：
public ListNode reverseList(ListNode head) {
if(head == null || head.next == null) { //终止条件并不难想
return head;
}
ListNode node = reverseList(head.next);
head.next.next = head;
head.next = null;
return node; //按上面的例子，F(node=1)和 F(node=2)它俩反转后的头节点是同一个
}



## 回溯知识点

一定不要一下子解决某一问题，一定不要有这种想法
分段分时的进行分解，解决当前的问题就可以！！！！

## 判断坐标是否在同一对角线

(currentRow + currentCol === row + col || currentRow - currentCol === row - col )
