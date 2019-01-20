import re	
class Finite_state_Machine:
	def __init__(self): 
		self.handlers = {}
		self.startState = None
		self.endStates = []
	# 参数name为状态名,handler为状态转移函数,end_state表明是否为最终状态
	def add_state(self, name, handler, end_state=0):
		name = name.upper() # 转换为大写
		self.handlers[name] = handler
		if end_state:
			self.endStates.append(name)

	def set_start(self, name):
		self.startState = name.upper()

	def run(self, cargo):
		try:
			handler = self.handlers[self.startState]
		except:
			raise InitializationError("must call .set_start() before .run()")
		if not self.endStates:
			raise  InitializationError("at least one state must be an end_state")
		
		# 从Start状态开始进行处理
		while True: 
			(newState, cargo) = handler(cargo)    # 经过状态转移函数变换到新状态
			if newState.upper() in self.endStates: # 如果跳到终止状态,则打印状态并结束循环
				print("reached ", newState)

				if newState=="error_state":
					print("false")
					return False
				else:
					print("true")
					return True
			else:                        # 否则将转移函数切换为新状态下的转移函数 
				handler = self.handlers[newState.upper()]  # liquid

	# def handler(cargo):
	# 	state=self.start_transitions(cargo)
	# 	return (state, cargo)



# 自定义状态转变函数
	def start_transitions(self,txt):
		# 过指定分隔符对字符串进行切片,默认为空格分割,参数num指定分割次数
		# 将"Python is XXX"语句分割为"Python"和之后的"is XXX"
		splitted_txt = txt.split('.')  
		splitted_txt1=txt.split('e')
		print("split .:", splitted_txt)
		print("split e:", splitted_txt1)

		if len(splitted_txt)==1 and len(splitted_txt1)==1:
			print("1st level", splitted_txt)
			if self.number_check(splitted_txt):
				newState="Integer_state"
			else:
				print("aaaaa")
				newState="error_state"
		elif len(splitted_txt)==2:
			if self.number_check(splitted_txt):
				newState="Float_state"
			else:
				newState="error_state"
		elif len(splitted_txt1)==2:
			if not splitted_txt1[0]=='' or splitted_txt1[1]=='':
				if self.number_check(splitted_txt1):
					newState="Scientific_number_state"
				else:
					newState="error_state"
			else:
				newState="error_state"
		else :
			newState="error_state"
		return (newState, txt)        # 返回新状态和余下的语句txt

	def number_check(self,alist):
		print(alist,"length is",len(alist))
		if len(alist)<=2 and len(alist)!=0:
			for element in alist:
				print("element is",element )
				if not re.match('^\d*$',element):
					return False
			print("hahah")
			return True
		else:
			return False




if __name__== "__main__":
	m=Number()
	m.add_state("Start", m.start_transitions)      # 添加初始状态
	m.add_state("Integer_state", None, end_state=1)  # 添加最终状态
	m.add_state("Float_state", None, end_state=1)
	m.add_state("Scientific_number_state",None,end_state=1)
	m.add_state("error_state", None, end_state=1)
	
	m.set_start("Start") # 设置开始状态
	m.run("0")
	m.run("32.56")
	m.run("e10")
