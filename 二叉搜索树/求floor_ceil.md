寻找一个元素的floor and ceil,这个元素可以不在树里


rank()  //给出一个元素问它的排名是第几

select()  // select是rank的反向，返回排名是第几的元素



维护size的bst可以让求rank和select的操作容易很多


维护depth的bst


支持重复元素的bst //左子树<=root, 右子树>=root

对于重复元素的bst还可以在节点里面多记录一个信息，记录当前节点的元素在树中有多少个（计数）


bst的很多题目都是在node中维护一些多余的信息
