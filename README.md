#### اضافة عميل جديد

<img src="[https://github.com/Gouda01/gouda01/blob/main/Web%20Development.jpg](https://github.com/melazab960/Main/blob/main/0.jpg)" align="center" style="width: 100%" />

```python
def save(self, *args, **kwargs):
        self.slug = slugify(self.name)

        
        if self.pk:      # اذا كان المنتج موجود بالفعل 
            try:
                old_instance = Product.objects.get(pk=self.pk)    #  هات المنتج القديم   
                if old_instance.brand != self.brand or old_instance.mainitem  != self.mainitem:    #  هل البراند والبند الرئيسي الجديد لا يساوي القديم معني كده حصل تعديل في ايهم 
                   self.code = f"{self.mainitem.code}-{self.brand.code}-{old_instance.code_no}"   # سجل الكود مره تانية بالبيانات الجديدة

            except Product.DoesNotExist:
                pass
        

        elif not self.code:
            last_product = Product.objects.filter(
                mainitem=self.mainitem,
                brand=self.brand
            ).order_by('-id').first()

            if last_product and last_product.code and last_product.code_no:
                

                next_number = int(last_product.code_no) + 1 


            else:
                next_number = 1

            self.code = f"{self.mainitem.code}-{self.brand.code}-{next_number}"
            self.code_no=next_number

        
        

        super().save(*args, **kwargs)
```


