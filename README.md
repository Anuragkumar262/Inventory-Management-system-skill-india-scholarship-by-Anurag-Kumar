# Inventory-Management-system-skill-india-scholarship-by-Anurag-Kumar
skill india elite techno group inventory management




import json
import datetime
print("-------Welcome to Inventory-------")
print()
print("Main Menu  ")
print("1. Add in Inventory\n2.Search in Inventory\n3.Purchase Product")
ch=int(input("Enter Your Choice:  "))

def add():
  fd=open("prod.json",'r')
  r=fd.read()
  fd.close()
  rec=json.loads(r)
  id=input("Enter prod id: ")
  quant=int(input("Enter quantity of prod.: "))
  rec[id]["qn"]+=quant
  js1=json.dumps(rec)
  fd1=open("prod.json",'w')
  fd1.write(js1)
  fd1.close()
def ser():
  newser=open("prod.json",'r')
  qser=newser.read()
  newser.close()
  out=json.loads(qser)
  serw=input("Enter product id you want to search: ")
  print("Prod. I'd\t\tName\tPrice\t\tQuantity\t\tRating\t\tType\t\tNet Wgt.")
  if  serw in out.keys():
    print(serw,'\t\t  ',out[serw]["name"],'\t',out[serw]["pr"],'\t\t',out[serw]["qn"],'\t\t\t',out[serw]["rating"],'\t\t',out[serw]["type"],'\t',out[serw]["net_wt(gm)"])
  else:
    print("This product is not available")

def pur():
  con=open("prod.json",'r')
  pur=con.read()
  con.close()
  sell=json.loads(pur)
  ch="y"
  nameyou=input("Enter Your Namne: ")
  phyou=(input("Enter Your phone no: "))

  dat=datetime.datetime.now()
  day=str(dat.day)
  mon=str(dat.month)
  yr=str(dat.year)
  date=(day+"-"+mon+"-"+"-"+yr)
  hr=str(dat.hour)
  mn=str(dat.minute)
  sc=str(dat.second)
  time=(hr+":"+mn+":"+sc)
  totalamt=0
  while ch=="y" or ch=="Y":
    num=input("Enter Product I'd you want to purchase: ")
    
    print("Prod. I'd\t\tName\tPrice\t\tQuantity\t\tRating\t\tType\t\tNet Wgt.")
    print(num,'\t\t  ',sell[num]["name"],'\t',sell[num]["pr"],'\t\t',sell[num]["qn"],'\t\t\t',sell[num]["rating"],'\t\t',sell[num]["type"],'\t',sell[num]["net_wt(gm)"])
    quty_pur=int(input("Enter the quantity you want to purchase"))
    if quty_pur<=sell[num]["qn"]:
        sell[num]["qn"]-=quty_pur
        totalamt+=(quty_pur*sell[num]["pr"])
        print("purchse succesful")
    else:
        print("Quantity is less available for this product\nDo you want to purchase ",sell[num]["qn"]," quantity of ",sell[num]["name"])
        print("1. Yes\n2. No")
        user=int(input("Enter your choice: "))
        if user==1:
          sell[num]["qn"]-=sell[num]["qn"]
          totalamt+=(sell[num]["qn"]*sell[num]["pr"])
          print("purchse succesful")
        else:
          print("Thank You For Shopping ")
    print("Do You Want to continue for purchasing another product(Y or N)")
    nexpur=input("Enter Your Choice :")
    ch=nexpur
    res=open("sales.json",'r')
    rep=res.read()
    res.close()
    new=json.loads(rep)
  
    new[phyou]={"name":nameyou,"Total":totalamt,"date":date,"time":time}
    dup=json.dumps(new)  

    bi=open("sales.json",'w')
    bi.write(dup)
    bi.close()

    up=json.dumps(sell)

    op=open("prod.json",'w')
    op.write(up)
    op.close()
    continue
if ch==1:
  add()
elif ch==2:
  ser()
elif ch==3:
  pur()
  
  
  
  
