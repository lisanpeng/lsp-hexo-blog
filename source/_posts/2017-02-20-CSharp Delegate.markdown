---
title:  "C# 带参数的delegate"
categories: C#
tags: C# delegate
---

记录了C#中带有参数的delegate的使用，委托的定义及调用。
<!--more-->
```s

//带有参数的委托声明
private delegate void addItems2ListboxEventhandler(string path);

//调用委托
private void addItems2Listbox()
{
  try
  {
    while (startAdd2List)
    {
      if (fileAL.Count > 0)
      {
        if (listBoxMsg.InvokeRequired)
        {
          //带有参数的委托调用
          listBoxMsg.Invoke(new addItems2ListboxEventhandler(addContents), new object[]{ fileAL[0].ToString() });
        }
        fileAL.RemoveAt(0);
      }
      Thread.Sleep(10);
    }
  }
  catch (Exception ex)
  {
    MessageBox.Show("addItems2ListboxEventhandler() " + ex.ToString());
  }
}

//实现方法
private void addContents(string filePath)
{
  try
  {
    if(listBoxMsg.Items.Count > 20)
    {
      listBoxMsg.Items.Clear();
    }
    string contents = msgReader(filePath);
    if (contents.Length > 20)
    {
      listBoxMsg.Items.Insert(0,contents);
    }
  }
  catch (Exception ex)
  {
    MessageBox.Show("addContents(string filePath) " + ex.ToString());
  }
}

```
