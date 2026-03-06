# Leetcode-CPP-
链表

1......移除链表元素
给你一个链表的头节点 head 和一个整数 val ，请你删除链表中所有满足 Node.val == val 的节点，并返回 新的头节点 。
 

示例 1：


输入：head = [1,2,6,3,4,5,6], val = 6
输出：[1,2,3,4,5]
示例 2：

输入：head = [], val = 1
输出：[]
示例 3：

输入：head = [7,7,7,7], val = 7
输出：[]




///////注意 ->val 指的是指向目标是其中的值 ->next的意思是对象是下一个存储单元，不是指向值
struct ListNode* removeElements(struct ListNode* head, int val){  //，功能是删除链表中所有值等于val的节点。
                                                                   ////入参：head是链表的头节点，val是要删除的目标值。
                                                                    ////返回值：处理完的新链表的头节点指针。
    struct ListNode* temp;    ////提前定义一个临时指针，后面所有要删除的节点，都会先把地址存在这里，方便后续释放内存。
    
    while(head && head->val == val) ////    // 当头结点存在并且头结点的值等于val时/////注意->val全名value指的是存储在head里面的值而不是 要剔除的目标数(==val)
    {
        temp = head;
        // 将新的头结点设置为head->next并删除原来的头结点
        head = head->next;
        free(temp);
    }

    struct ListNode *cur = head;   //把cur初始化为处理完头节点后的新head，也就是从合法的链表起点开始遍历。
    // 当cur存在并且cur->next存在时   意思是不等于NULL  而不是里面的值val等不等于0
    // 此解法需要判断cur存在因为cur指向head。若head本身为NULL或者原链表中元素都为val的话，cur也会为NULL
    while(cur && (temp = cur->next)) {
        // 若cur->next的值等于val
        if(temp->val == val) {
            // 将cur->next设置为cur->next->next并删除cur->next  
            cur->next = temp->next;
            free(temp);
        }
        // 若cur->next不等于val，则将cur后移一位
        else
            cur = cur->next;
    }

    // 返回头结点
    return head;
}   //
