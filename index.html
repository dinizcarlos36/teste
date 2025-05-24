class AgendamentoSystem {
    constructor() {
        this.agendamentos = JSON.parse(localStorage.getItem('agendamentos')) || [];
        this.currentWeek = new Date();
        this.isAdminLoggedIn = false;
        this.init();
    }

    init() {
        this.setupEventListeners();
        this.renderCalendar();
        this.updateFilters();
        this.showSection('homeSection');
        this.setMinDate();
    }

    setupEventListeners() {
        // Navigation
        document.getElementById('btnHome').addEventListener('click', () => this.showSection('homeSection'));
        document.getElementById('btnCalendar').addEventListener('click', () => this.showSection('calendarSection'));
        document.getElementById('btnAdmin').addEventListener('click', () => this.showSection('adminSection'));

        // Form submission
        document.getElementById('agendamentoForm').addEventListener('submit', (e) => this.handleFormSubmit(e));

        // Admin login
        document.getElementById('loginForm').addEventListener('submit', (e) => this.handleAdminLogin(e));

        // Calendar navigation
        document.getElementById('prevWeek').addEventListener('click', () => this.navigateWeek(-1));
        document.getElementById('nextWeek').addEventListener('click', () => this.navigateWeek(1));

        // Filters
        document.getElementById('filterEspaco').addEventListener('change', () => this.applyFilters());
        document.getElementById('filterProfessor').addEventListener('change', () => this.applyFilters());
        document.getElementById('filterSerie').addEventListener('change', () => this.applyFilters());

        // Modal
        document.querySelector('.close').addEventListener('click', () => this.closeModal());
        document.getElementById('modalCancel').addEventListener('click', () => this.closeModal());
    }

    setMinDate() {
        const today = new Date().toISOString().split('T')[0];
        document.getElementById('data').setAttribute('min', today);
    }

    showSection(sectionId) {
        // Hide all sections
        document.querySelectorAll('.section').forEach(section => {
            section.classList.remove('active');
        });

        // Remove active class from nav buttons
        document.querySelectorAll('.nav-btn').forEach(btn => {
            btn.classList.remove('active');
        });

        // Show selected section
        document.getElementById(sectionId).classList.add('active');

        // Add active class to corresponding nav button
        if (sectionId === 'homeSection') {
            document.getElementById('btnHome').classList.add('active');
        } else if (sectionId === 'calendarSection') {
            document.getElementById('btnCalendar').classList.add('active');
            this.renderCalendar();
            this.renderAgendamentosList();
        } else if (sectionId === 'adminSection') {
            document.getElementById('btnAdmin').classList.add('active');
            if (this.isAdminLoggedIn) {
                this.showAdminPanel();
            }
        }
    }

    handleFormSubmit(e) {
        e.preventDefault();
        
        const formData = new FormData(e.target);
        const agendamento = {
            id: Date.now(),
            professor: formData.get('professor'),
            espaco: formData.get('espaco'),
            serie: formData.get('serie'),
            data: formData.get('data'),
            horaInicio: formData.get('horaInicio'),
            horaFim: formData.get('horaFim'),
            created: new Date().toISOString()
        };

        // Validate time
        if (agendamento.horaInicio >= agendamento.horaFim) {
            this.showAlert('O horário de início deve ser anterior ao horário de término.', 'error');
            return;
        }

        // Check for conflicts
        if (this.hasConflict(agendamento)) {
            this.showAlert('Já existe um agendamento para este espaço no horário selecionado.', 'error');
            return;
        }

        // Save agendamento
        this.agendamentos.push(agendamento);
        this.saveToStorage();
        
        this.showAlert('Ensaio agendado com sucesso!', 'success');
        e.target.reset();
        this.updateFilters();
    }

    hasConflict(newAgendamento) {
        return this.agendamentos.some(agendamento => {
            if (agendamento.espaco !== newAgendamento.espaco || agendamento.data !== newAgendamento.data) {
                return false;
            }

            const existingStart = agendamento.horaInicio;
            const existingEnd = agendamento.horaFim;
            const newStart = newAgendamento.horaInicio;
            const newEnd = newAgendamento.horaFim;

            return (newStart < existingEnd && newEnd > existingStart);
        });
    }

    renderCalendar() {
        const calendar = document.getElementById('calendar');
        calendar.innerHTML = '';

        // Get start of week (Monday)
        const startOfWeek = new Date(this.currentWeek);
        startOfWeek.setDate(startOfWeek.getDate() - startOfWeek.getDay() + 1);

        // Update week display
        const endOfWeek = new Date(startOfWeek);
        endOfWeek.setDate(endOfWeek.getDate() + 6);
        
        document.getElementById('currentWeek').textContent = 
            `${startOfWeek.toLocaleDateString('pt-BR')} - ${endOfWeek.toLocaleDateString('pt-BR')}`;

        // Add day headers
        const dayNames = ['Segunda', 'Terça', 'Quarta', 'Quinta', 'Sexta', 'Sábado', 'Domingo'];
        dayNames.forEach(day => {
            const dayHeader = document.createElement('div');
            dayHeader.className = 'calendar-day header';
            dayHeader.textContent = day;
            calendar.appendChild(dayHeader);
        });

        // Add days
        for (let i = 0; i < 7; i++) {
            const currentDay = new Date(startOfWeek);
            currentDay.setDate(currentDay.getDate() + i);
            
            const dayElement = document.createElement('div');
            dayElement.className = 'calendar-day';
            
            const dateElement = document.createElement('div');
            dateElement.className = 'date';
            dateElement.textContent = currentDay.getDate();
            dayElement.appendChild(dateElement);

            // Add ensaios for this day
            const dayString = currentDay.toISOString().split('T')[0];
            const dayAgendamentos = this.getFilteredAgendamentos().filter(agendamento => agendamento.data === dayString);
            
            dayAgendamentos.forEach(agendamento => {
                const ensaioElement = document.createElement('div');
                ensaioElement.className = 'ensaio-item';
                ensaioElement.innerHTML = `
                    <div>${agendamento.horaInicio} - ${agendamento.horaFim}</div>
                    <div>${agendamento.professor}</div>
                    <div>${agendamento.espaco}</div>
                `;
                ensaioElement.addEventListener('click', () => this.showAgendamentoDetails(agendamento));
                dayElement.appendChild(ensaioElement);
            });

            calendar.appendChild(dayElement);
        }
    }

    navigateWeek(direction) {
        this.currentWeek.setDate(this.currentWeek.getDate() + (direction * 7));
        this.renderCalendar();
    }

    renderAgendamentosList() {
        const list = document.getElementById('agendamentosList');
        const agendamentos = this.getFilteredAgendamentos()
            .filter(agendamento => new Date(agendamento.data) >= new Date())
            .sort((a, b) => new Date(a.data + ' ' + a.horaInicio) - new Date(b.data + ' ' + b.horaInicio))
            .slice(0, 10);

        if (agendamentos.length === 0) {
            list.innerHTML = '<p>Nenhum ensaio agendado.</p>';
            return;
        }

        list.innerHTML = agendamentos.map(agendamento => `
            <div class="agendamento-card">
                <div class="header">
                    <div class="title">${agendamento.professor}</div>
                    <div class="badge">${agendamento.espaco}</div>
                </div>
                <div class="details">
                    <div><i class="fas fa-graduation-cap"></i> ${agendamento.serie}</div>
                    <div><i class="fas fa-calendar"></i> ${new Date(agendamento.data).toLocaleDateString('pt-BR')}</div>
                    <div><i class="fas fa-clock"></i> ${agendamento.horaInicio} às ${agendamento.horaFim}</div>
                </div>
            </div>
        `).join('');
    }

    updateFilters() {
        const professores = [...new Set(this.agendamentos.map(a => a.professor))].sort();
        const series = [...new Set(this.agendamentos.map(a => a.serie))].sort();

        // Update professor filter
        const professorFilter = document.getElementById('filterProfessor');
        const currentProfessor = professorFilter.value;
        professorFilter.innerHTML = '<option value="">Todos os professores</option>';
        professores.forEach(professor => {
            const option = document.createElement('option');
            option.value = professor;
            option.textContent = professor;
            if (professor === currentProfessor) option.selected = true;
            professorFilter.appendChild(option);
        });

        // Update serie filter
        const serieFilter = document.getElementById('filterSerie');
        const currentSerie = serieFilter.value;
        serieFilter.innerHTML = '<option value="">Todas as séries</option>';
        series.forEach(serie => {
            const option = document.createElement('option');
            option.value = serie;
            option.textContent = serie;
            if (serie === currentSerie) option.selected = true;
            serieFilter.appendChild(option);
        });
    }

    applyFilters() {
        this.renderCalendar();
        this.renderAgendamentosList();
    }

    getFilteredAgendamentos() {
        const espacoFilter = document.getElementById('filterEspaco').value;
        const professorFilter = document.getElementById('filterProfessor').value;
        const serieFilter = document.getElementById('filterSerie').value;

        return this.agendamentos.filter(agendamento => {
            return (!espacoFilter || agendamento.espaco === espacoFilter) &&
                   (!professorFilter || agendamento.professor === professorFilter) &&
                   (!serieFilter || agendamento.serie === serieFilter);
        });
    }

    handleAdminLogin(e) {
        e.preventDefault();
        const password = document.getElementById('adminPassword').value;
        
        if (password === 'admin123') {
            this.isAdminLoggedIn = true;
            this.showAdminPanel();
        } else {
            this.showAlert('Senha incorreta!', 'error');
        }
    }

    showAdminPanel() {
        document.getElementById('adminLogin').style.display = 'none';
        document.getElementById('adminPanel').style.display = 'block';
        
        this.updateAdminStats();
        this.renderAdminAgendamentos();
    }

    updateAdminStats() {
        const today = new Date().toISOString().split('T')[0];
        const agendamentosHoje = this.agendamentos.filter(a => a.data === today).length;
        
        document.getElementById('totalAgendamentos').textContent = this.agendamentos.length;
        document.getElementById('agendamentosHoje').textContent = agendamentosHoje;
    }

    renderAdminAgendamentos() {
        const list = document.getElementById('adminAgendamentosList');
        const sortedAgendamentos = [...this.agendamentos].sort((a, b) => 
            new Date(b.data + ' ' + b.horaInicio) - new Date(a.data + ' ' + a.horaInicio)
        );

        list.innerHTML = sortedAgendamentos.map(agendamento => `
            <div class="admin-agendamento">
                <div>
                    <strong>${agendamento.professor}</strong> - ${agendamento.serie}<br>
                    <small>${agendamento.espaco} | ${new Date(agendamento.data).toLocaleDateString('pt-BR')} | ${agendamento.horaInicio} - ${agendamento.horaFim}</small>
                </div>
                <div class="admin-actions">
                    <button class="btn-edit" onclick="agendamentoSystem.editAgendamento(${agendamento.id})">
                        <i class="fas fa-edit"></i> Editar
                    </button>
                    <button class="btn-delete" onclick="agendamentoSystem.deleteAgendamento(${agendamento.id})">
                        <i class="fas fa-trash"></i> Excluir
                    </button>
                </div>
            </div>
        `).join('');
    }

    editAgendamento(id) {
        const agendamento = this.agendamentos.find(a => a.id === id);
        if (!agendamento) return;

        // Pre-fill form with agendamento data
        document.getElementById('professor').value = agendamento.professor;
        document.getElementById('espaco').value = agendamento.espaco;
        document.getElementById('serie').value = agendamento.serie;
        document.getElementById('data').value = agendamento.data;
        document.getElementById('horaInicio').value = agendamento.horaInicio;
        document.getElementById('horaFim').value = agendamento.horaFim;

        // Remove the agendamento temporarily for conflict checking
        this.agendamentos = this.agendamentos.filter(a => a.id !== id);
        this.saveToStorage();

        // Switch to home section
        this.showSection('homeSection');
        
        this.showAlert('Agendamento carregado para edição. Faça as alterações e salve novamente.', 'success');
    }

    deleteAgendamento(id) {
        this.showModal(
            'Confirmar Exclusão',
            'Tem certeza que deseja excluir este agendamento?',
            () => {
                this.agendamentos = this.agendamentos.filter(a => a.id !== id);
                this.saveToStorage();
                this.renderAdminAgendamentos();
                this.updateAdminStats();
                this.updateFilters();
                this.showAlert('Agendamento excluído com sucesso!', 'success');
                this.closeModal();
            }
        );
    }

    showAgendamentoDetails(agendamento) {
        this.showModal(
            'Detalhes do Ensaio',
            `
            <strong>Professor:</strong> ${agendamento.professor}<br>
            <strong>Série:</strong> ${agendamento.serie}<br>
            <strong>Espaço:</strong> ${agendamento.espaco}<br>
            <strong>Data:</strong> ${new Date(agendamento.data).toLocaleDateString('pt-BR')}<br>
            <strong>Horário:</strong> ${agendamento.horaInicio} às ${agendamento.horaFim}
            `,
            null,
            false
        );
    }

    showModal(title, message, onConfirm = null, showActions = true) {
        document.getElementById('modalTitle').textContent = title;
        document.getElementById('modalMessage').innerHTML = message;
        
        const actions = document.querySelector('.modal-actions');
        if (showActions && onConfirm) {
            actions.style.display = 'flex';
            document.getElementById('modalConfirm').onclick = onConfirm;
        } else {
            actions.style.display = showActions ? 'flex' : 'none';
        }
        
        document.getElementById('modal').style.display = 'block';
    }

    closeModal() {
        document.getElementById('modal').style.display = 'none';
    }

    showAlert(message, type) {
        // Remove existing alerts
        document.querySelectorAll('.alert').forEach(alert => alert.remove());
        
        const alert = document.createElement('div');
        alert.className = `alert ${type}`;
        alert.innerHTML = `<i class="fas fa-${type === 'success' ? 'check-circle' : 'exclamation-circle'}"></i> ${message}`;
        
        const form = document.getElementById('agendamentoForm');
        form.parentNode.insertBefore(alert, form);
        
        setTimeout(() => alert.remove(), 5000);
    }

    saveToStorage() {
        localStorage.setItem('agendamentos', JSON.stringify(this.agendamentos));
    }
}

// Initialize the system
const agendamentoSystem = new AgendamentoSystem();
