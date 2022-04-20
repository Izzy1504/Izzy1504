#include<iostream>
using namespace std;
// khai báo cấu trúc 1 cái node trong cây nhị phân tìm kiếm
struct node
{
    int data; 
    struct node *pLeft; 
    struct node *pRight; 
};
typedef struct node NODE;
typedef NODE* TREE;
  
// hàm khởi tạo cây nhị phân tìm kiếm
void KhoiTaoCay(TREE &t)
{
    t = NULL;
}
  
// hàm thêm 1 cái phần tử vào cây
void ThemNodeVaoCay(TREE &t, int x)
{
    // nếu cây rỗng
    if (t == NULL)
    {
        NODE *p = new NODE;
        p->data = x;
        p->pLeft = NULL;
        p->pRight = NULL;
        t = p;
    }
    else
    {
        // nếu phần tử thêm vào mà nhỏ hơn nút gốc thì sẽ duyệt qua bên trái
        if (x < t->data)
        {
            ThemNodeVaoCay(t->pLeft, x);
        }
        else if (x > t->data)
        {
            ThemNodeVaoCay(t->pRight, x);
        }
    }
}
  
// hàm xuất phần tử trong cây nhị phân tìm kiếm
void NLR(TREE t)
{
    if (t != NULL)
    {
        // xử lí
        cout << t->data << "  ";
        NLR(t->pLeft);
        NLR(t->pRight);
    }
}
void NRL(TREE t)
{
    if(t != NULL)
    {
        cout << t->data << "  ";
        NLR(t->pRight);
        NLR(t->pLeft);

    }
}  
 void LNR(TREE t)
 {
     if(t != NULL)
     {
         LNR(t->pLeft);
         cout<< t->data << "  ";
         LNR(t->pRight);
     }
 }
 void RNL(TREE t)
 {
     if(t != NULL)
     {
     RNL(t->pRight);
     cout << t->data << "  ";
     RNL(t->pLeft);
     }
 }
 NODE* search(TREE t, int x)
 {
     if(t == NULL)
     {
         return NULL;
     }
     else
     {
         if(x< t->data)
         {
             search(t->pLeft,x);
         }
         else if(x> t->data)
         {
             search(t->pRight,x);
         }
         else
         {
             return t;
         }
     } 
}
// hàm tìm node thế mạng
void NodeTheMang(TREE &X, TREE &Y)
{
    if (Y->pLeft != NULL)
    {
        NodeTheMang(X, Y->pLeft);
    }
    else 
    {
        X->data = Y->data; 
        X = Y; 
        Y = Y->pRight; 
    }
 
}
 

void XoaNode(TREE &t, int data) 
{
    
    if (t == NULL)
    {
        return;
    }
    else
    {
        if (data < t->data)
        {
            XoaNode(t->pLeft, data);
        }
        else if (data > t->data)
        {
            XoaNode(t->pRight, data); 
        }
        else 
        {
            NODE *X = t;
            if (t->pLeft == NULL)
            {
               
                t = t->pRight; 
            }
            else if (t->pRight == NULL)
            {
                
                t = t->pLeft;
            }
            else 
            {
                
                NodeTheMang(X, t->pRight);
                //CÁCH 2: Tìm node phải nhất của cây con trái(cây con trái của cái node cần xóa)
                //DiTimNodeTheMang(X, t->pLeft);
            }
            delete X;
        }
    }
}
  
// hàm nhập cây nhị phân tìm kiếm
void Menu(TREE &t)
{
    int luachon;
    while(true)
    {
        cout << "\n\n\t\t ============ MENU ============";
        cout << "\n1. Nhap phan tu cho cay";
        cout << "\n2. Duyet cay theo NLR";
        cout << "\n3. Duyet cay theo RNL";
        cout << "\n4. Duyet cay theo LNR";
        cout << "\n5. Duyet cay theo RNL";
        cout << "\n6. Xoa bat ki ";
        cout << "\n7. Tim kiem";
        cout << "\n0. Thoat";
        cout << "\n\n\t\t =============  END  =============";
  
        cout << "\nNhap lua chon : ";
        cin >> luachon;
  
        if (luachon == 1)
        {
            int x;
            cout << "\nNhap gia tri: ";
            cin >> x;
            ThemNodeVaoCay(t, x);
        }
        else if (luachon == 2)
        {
            cout << "\nCay nhi phan duyet theo\n";
            NLR(t);
        }
        else if(luachon == 3)
        {
            cout <<"\nCay nhi phan duyet theo RNL\n";
            RNL(t);
        }
        else if(luachon == 4)
        {
            cout << "\nCay nhi phan duyet theo LNR\n";
            LNR(t);
        }
        else if(luachon == 5)
        {
            cout << "\nCay nhi phan duyet theo RNL\n";
            RNL(t);
        }
        else if (luachon == 6)
            {
                  int x;
                cout << "\nNhap gia tri can xoa: ";
                cin >> x;
                XoaNode(t, x);
            }
        else if (luachon == 7)
        {
            int x;
            cout<<"\nNhap gia tri can tim kiem: ";
            cin>>x;
            NODE* p=search(t, x);
            if(p==NULL)
            {
            cout<<"khong co phan tu";
            }
            else
            cout<<"Phan tu "<<x<<" nam o vi tri "<<p;
        }
        else
        {
            break;
        }
    }
}
 
  
int main()
{
    TREE t;
    KhoiTaoCay(t);
    Menu(t);
  
    cout<<"\n---------------------------------\n";
}
