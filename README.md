Cd newspaper

Создаем миграцию

py manage.py makemigrations

Осуществляем миграцию

py manage.py migrate

Переходим в консоль Python

py manage.py shell

Импортируем модлеи

from news.models import *

Создаем пользователей

u1 = User.objects.create_user(username='Ivan')
u2 = User.objects.create_user(username='Roman')
u3 = User.objects.create_user(username='Divan') 
u4 = User.objects.create_user(username='Stakan')

Создаем авторов

Author.objects.create(authorUser=u1)
Author.objects.create(authorUser=u4) 

Создаем категории

Category.objects.create(name='IT')
Category.objects.create(name='BT')
Category.objects.create(name='AT')
Category.objects.create(name='PT')

Создаем Статьи

Author1 = Author.objects.get(id=1)
Author4 = Author.objects.get(id=2)
Post.objects.create(author=Author1, categoryType='NW', title='sometitle', text='somebigtext') 
Post.objects.create(author=Author4, categoryType='AR', title='anytitle', text='text')
Post.objects.create(author=Author1, categoryType='AR', title='title', text='litletext')
Post.objects.create(author=Author4, categoryType='BT',  title='title', text='litletext')

Присваиваем Категории статьям

Post.objects.get(id=1).postCategory.add(Category.objects.get(id=1))
Post.objects.get(id=1).postCategory.add(Category.objects.get(id=2))

Создаем комментарии

Comment.objects.create(commentPost=Post.objects.get(id=1), commentUser=Author.objects.get(id=1).authorUser, text='anytextbyauthor')
Comment.objects.create(commentPost=Post.objects.get(id=2), commentUser=Author.objects.get(id=2).authorUser, text='anytextbyauthor')
Comment.objects.create(commentPost=Post.objects.get(id=3), commentUser=Author.objects.get(id=3).authorUser, text='anytextbyauthor')
Comment.objects.create(commentPost=Post.objects.get(id=1), commentUser=Author.objects.get(id=3).authorUser, text='anytextbyauthor')
Comment.objects.create(commentPost=Post.objects.get(id=4), commentUser=Author.objects.get(id=1).authorUser, text='anytextbyauthor')

Корректируем рейтинги

Comment.objects.get(id=1).like()
Comment.objects.get(id=1).like()
Comment.objects.get(id=2).like()  
Comment.objects.get(id=3).like() 
Comment.objects.get(id=4).like() 
Comment.objects.get(id=5).like() 
Comment.objects.get(id=3).like()
Comment.objects.get(id=1).dislike() 
Comment.objects.get(id=1).dislike() 
Comment.objects.get(id=3).dislike()  
Comment.objects.get(id=5).dislike() 
Post.objects.get(id=1).like()
Post.objects.get(id=2).like()  
Post.objects.get(id=2).like() 
Post.objects.get(id=3).dislike()
Post.objects.get(id=5).dislike()

Обновляем Рейтинги

Author1.update_rating()
Author4.update_rating()

Выводим username и рейтинг лучшего пользователя (применяя сортировку и возвращая поля первого объекта)

B = Author.objects.all().order_by('-ratingAuthor').values('authorUser', 'ratingAuthor')[0]

Выводим дату добавления, username автора, рейтинг, заголовок и превью лучшей статьи, основываясь на лайках/дислайках к этой статье

Post.objects.all().order_by('-rating').values('dateCreation', 'postAuthor__authorUser__username', 'rating', 'preview_name', 'text')[0]

Выводим все комментарии (дата, пользователь, рейтинг, текст) к этой статье

Comment.objects.all().order_by().values('dateCreation', 'commentUser__username', 'commentPost', 'rating', 'commentText')[0]
Post.objects.all().values('postAuthor', 'preview_name') Post.objects.filter(postAuthor=author02) Post.objects.filter(preview_name='Заголовок_статьи_1').values('postAuthor')
Comment.objects.all().values('commentPost', 'commentUser') Comment.objects.filter(commentPost=article01).values('commentText') Comment.objects.filter(commentText='Текст_статьи_комментария_2').values('rating')
Author.objects.filter(id=1). Author.objects.all().values('authorUser', 'id')
