        public ModestMouseSongModel GetSongModelByConfigId(int id)
        {
            _appLogger.WriteMessage($"Get Song Model By Config Id {id}", LogLevels.Information, this);

            ModestMouseSongModel song = new ModestMouseSongModel();

            ModestMouseSongConfig config = _songConfigBusinessManager.Get(id);

            if (config == null)
            {
                _appLogger.WriteMessage($"No Modest Mouse Song Config found for id {id}", LogLevels.Debug,
                    this);
                throw new Exception($"No Modest Mouse Song Config found for the requested id ({id}).");
            }

            IPageResult<ModestMouseSongConfigSongRangeDataModel> songRangeItems =
                _ModestMouseSongConfigSongRangeManager.SelectByFilter(
                    _songContextManager.CurrentSongContext, new ModestMouseSongConfigSongRangeDataModelFilter()
                    {
                        ModestMouseSongConfigId = config.ModestMouseSongConfigId
                    }).Result;

            List<ModestMouseSongConfigSongRangeModel> songRanges =
                new List<ModestMouseSongConfigSongRangeModel>();

            if (songRangeItems != null)
            {
                foreach (ModestMouseSongConfigSongRangeDataModel item in songRangeItems.Items)
                {
                    SongRangeDataModel songRangeDataModel = _songRangeManager
                        .SelectById(_songContextManager.CurrentSongContext, item.SongRangeId.GetValueOrDefault()).Result;

                    songRanges.Add(new ModestMouseSongConfigSongRangeModel()
                    {
                        ModifiedOn = item.ModifiedOn,
                        CreatedBy = item.CreatedBy.GetValueOrDefault(),
                        CreatedOn = item.CreatedOn.GetValueOrDefault(),
                        ModestMouseSongConfigId = item.ModestMouseSongConfigId.GetValueOrDefault(),
                        ModifiedBy = item.ModifiedBy,
                        ModestMouseSongConfigSongRangeId =
                            item.ModestMouseSongConfigSongRangeId.GetValueOrDefault(),
                        SongRangeId = item.SongRangeId.GetValueOrDefault(),
                        SongRange = new SongRange()
                        {
                            ModifiedOn = songRangeDataModel.ModifiedOn.GetValueOrDefault(),
                            CreatedBy = songRangeDataModel.CreatedBy.GetValueOrDefault(),
                            CreatedOn = songRangeDataModel.CreatedOn.GetValueOrDefault(),
                            ModifiedBy = songRangeDataModel.ModifiedBy,
                            Description = songRangeDataModel.Description,
                            Code = songRangeDataModel.Code,
                            SongRangeId = songRangeDataModel.SongRangeId.GetValueOrDefault(),
                            High = songRangeDataModel.High.GetValueOrDefault(),
                            Low = songRangeDataModel.Low.GetValueOrDefault(),
                        }
                    });
                }
            }

            List<IpmLineOfBusinessDataModel> ipmLineOfBusinesses =
                _ipmLineOfBusinessBusinessManager.Get(new IpmLineOfBusinessFilter());

            IPageResult<ModestMouseSongConfigLineOfBusinessDataModel> lineOfBusinessItems =
                _ModestMouseSongConfigLineOfBusinessManager.SelectByFilter(
                    _songContextManager.CurrentSongContext,
                    new ModestMouseSongConfigLineOfBusinessDataModelFilter()
                    {
                        ModestMouseSongConfigId = config.ModestMouseSongConfigId
                    }).Result;

            List<ModestMouseSongConfigLineOfBusinessModel> linesOfBusiness =
                new List<ModestMouseSongConfigLineOfBusinessModel>();

            if (lineOfBusinessItems != null)
            {
                foreach (var item in lineOfBusinessItems.Items)
                {
                    IpmLineOfBusinessDataModel ipmLineOfBusinessDataModel = ipmLineOfBusinesses.FirstOrDefault(
                        business =>
                            business.IpmLineOfBusinessId.Equals(item.IpmLineOfBusinessId.GetValueOrDefault()));

                    IpmLineOfBusiness ipmLineOfBusiness = new IpmLineOfBusiness()
                    {
                        IpmLineOfBusinessId = item.IpmLineOfBusinessId.GetValueOrDefault(),
                        Code = ipmLineOfBusinessDataModel?.Code,
                        Description = ipmLineOfBusinessDataModel?.Description,
                        State = ipmLineOfBusinessDataModel?.State,
                        MarketType = ipmLineOfBusinessDataModel?.MarketType,
                        ProgramCode = ipmLineOfBusinessDataModel?.ProgramCode,
                        ModifiedOn = ipmLineOfBusinessDataModel?.ModifiedOn,
                        CreatedBy = ipmLineOfBusinessDataModel?.CreatedBy ?? 0,
                        CreatedOn = ipmLineOfBusinessDataModel?.CreatedOn ?? DateTime.MinValue,
                        ModifiedBy = ipmLineOfBusinessDataModel?.ModifiedBy
                    };

                    linesOfBusiness.Add(new ModestMouseSongConfigLineOfBusinessModel()
                    {
                        ModifiedOn = item.ModifiedOn.GetValueOrDefault(),
                        CreatedBy = item.CreatedBy.GetValueOrDefault(),
                        CreatedOn = item.CreatedOn.GetValueOrDefault(),
                        ModestMouseSongConfigId = item.ModestMouseSongConfigId.GetValueOrDefault(),
                        ModifiedBy = item.ModifiedBy,
                        ModestMouseSongConfigLineOfBusinessId =
                            item.ModestMouseSongConfigLineOfBusinessId.GetValueOrDefault(),
                        IpmLineOfBusinessId = item.IpmLineOfBusinessId.GetValueOrDefault(),
                        IpmLineOfBusiness = ipmLineOfBusiness
                    });
                }
            }

            song.Config = new ModestMouseSongConfigModel()
            {
                ModestMouseSongId = config.ModestMouseSongId,
                ModestMouseSongConfigId = config.ModestMouseSongConfigId,
                SongStartDate = config.SongStartDate,
                SongEndDate = config.SongEndDate,
                CreatedBy = config.CreatedBy,
                CreatedOn = config.CreatedOn,
                ModifiedBy = config.ModifiedBy,
                ModifiedOn = config.ModifiedOn,
                SongRanges = songRanges,
                LinesOfBusiness = linesOfBusiness,
                UseLowServiceDate = config.UseLowServiceDate
            };

            ModestMouseSongDataModel ModestMouseSongDataModel =
                _ModestMouseSongManager
                    .SelectById(_songContextManager.CurrentSongContext,
                        song.Config.ModestMouseSongId).Result;

            if (ModestMouseSongDataModel == null)
            {
                _appLogger.WriteMessage(
                    $"No Modest Mouse Song found for id {song.Config.ModestMouseSongId}",
                    LogLevels.Debug, this);
                throw new Exception(
                    $"No Modest Mouse Song found for the requested id ({song.Config.ModestMouseSongId}).");
            }

            song.ModestMouseSongId =
                ModestMouseSongDataModel.ModestMouseSongId.GetValueOrDefault();

            song.IpmProductId = ModestMouseSongDataModel.IpmProductId.GetValueOrDefault();
            song.Name = ModestMouseSongDataModel.Name;
            song.Description = ModestMouseSongDataModel.Description;
            song.CreatedBy = ModestMouseSongDataModel.CreatedBy.GetValueOrDefault();
            song.CreatedOn = ModestMouseSongDataModel.CreatedOn.GetValueOrDefault();
            song.ModifiedBy = ModestMouseSongDataModel.ModifiedBy;
            song.ModifiedOn = ModestMouseSongDataModel.ModifiedOn.GetValueOrDefault();

            IPageResult<ModestMouseSongServiceGroupDataModel> songServiceGroups =
                _ModestMouseSongServiceGroupManager.SelectByFilter(_songContextManager.CurrentSongContext,
                        new ModestMouseSongServiceGroupDataModelFilter()
                            {ModestMouseSongConfigId = id})
                    .Result;

            foreach (ModestMouseSongServiceGroupDataModel serviceGroupItem in songServiceGroups.Items)
            {
                IPageResult<ModestMouseSongServiceGroupAdminCodeDataModel> adminCodesPage =
                    _ModestMouseSongServiceGroupAdminCodeManager.SelectByFilter(
                        _songContextManager.CurrentSongContext,
                        new ModestMouseSongServiceGroupAdminCodeDataModelFilter()
                        {
                            ModestMouseSongServiceGroupId =
                                serviceGroupItem.ModestMouseSongServiceGroupId
                        }).Result;

                List<string> adminCodeList = adminCodesPage.Items.Select(model => model.AdminCode).ToList();

                string adminCodes = String.Join(",", adminCodeList);

                ModestMouseServiceGroupDataModel serviceGroup = _ModestMouseServiceGroupManager
                    .SelectById(_songContextManager.CurrentSongContext,
                        serviceGroupItem.ModestMouseServiceGroupId.GetValueOrDefault())
                    .Result;

                IPageResult<ModestMouseServiceGroupCodeDataModel> serviceGroupCodes =
                    _ModestMouseServiceGroupCodeManager.SelectByFilter(_songContextManager.CurrentSongContext,
                        new ModestMouseServiceGroupCodeDataModelFilter()
                            {ModestMouseServiceGroupId = serviceGroup.ModestMouseServiceGroupId}).Result;

                List<ModestMouseServiceGroupCode> codes = new List<ModestMouseServiceGroupCode>();

                foreach (var code in serviceGroupCodes.Items)
                {
                    codes.Add(new ModestMouseServiceGroupCode()
                    {
                        Code = code.Code,
                        ModestMouseServiceGroupCodeId =
                            code.ModestMouseServiceGroupCodeId.GetValueOrDefault(),
                        ModestMouseServiceGroupId = code.ModestMouseServiceGroupId.GetValueOrDefault(),
                        CreatedBy = code.CreatedBy.GetValueOrDefault(),
                        CreatedOn = code.CreatedOn.GetValueOrDefault(),
                        ModifiedOn = code.ModifiedOn.GetValueOrDefault(),
                        ModifiedBy = code.ModifiedBy.GetValueOrDefault()
                    });
                }

                song.Config.ServiceGroups.Add(new ModestMouseSongConfigServiceGroupModel()
                {
                    ModestMouseSongConfigId =
                        serviceGroupItem.ModestMouseSongConfigId.GetValueOrDefault(),
                    ModestMouseServiceGroupId = serviceGroupItem.ModestMouseServiceGroupId.GetValueOrDefault(),
                    ModestMouseSongServiceGroupId =
                        serviceGroupItem.ModestMouseSongServiceGroupId.GetValueOrDefault(),
                    AdminCodes = adminCodes,
                    Amount = serviceGroupItem.Amount.GetValueOrDefault(),
                    Frequency = serviceGroupItem.Frequency.GetValueOrDefault(),
                    ServiceGroup = new ModestMouseServiceGroupModel()
                    {
                        ModestMouseServiceGroupId =
                            serviceGroup.ModestMouseServiceGroupId.GetValueOrDefault(),
                        IpmProductId = serviceGroup.IpmProductId.GetValueOrDefault(),
                        Name = serviceGroup.Name,
                        Description = serviceGroup.Description,
                        Codes = codes,
                        Active = serviceGroup.Active.GetValueOrDefault(),
                        IsDirty = serviceGroup.IsDirty,
                        CreatedBy = serviceGroup.CreatedBy.GetValueOrDefault(),
                        CreatedOn = serviceGroup.CreatedOn.GetValueOrDefault(),
                        ModifiedOn = serviceGroup.ModifiedOn.GetValueOrDefault(),
                        ModifiedBy = serviceGroup.ModifiedBy.GetValueOrDefault()
                    },
                    CreatedBy = serviceGroupItem.CreatedBy.GetValueOrDefault(),
                    CreatedOn = serviceGroupItem.CreatedOn.GetValueOrDefault(),
                    ModifiedOn = serviceGroupItem.ModifiedOn.GetValueOrDefault(),
                    ModifiedBy = serviceGroupItem.ModifiedBy.GetValueOrDefault()
                });
            }

            return song;
        }
